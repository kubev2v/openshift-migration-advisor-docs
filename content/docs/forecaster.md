---
title: "Migration Forecaster"
linkTitle: "Migration Forecaster"
description: "Benchmark storage throughput between VMware datastore pairs to forecast migration time"
weight: 4
---

# Migration Forecaster

The Migration Forecaster measures actual storage throughput between VMware datastore pairs by running disk-copy benchmarks directly on your vCenter infrastructure. The results provide data-driven migration time estimates based on your real environment rather than theoretical calculations.

Applies to: V0.11.0
Last update (dd-mm-yyyy): 03-05-2026

---

## How It Works

The forecaster creates **temporary resources** in your vCenter environment to benchmark disk copy speed between a source and target datastore. It repeats the copy multiple times and computes statistics (mean, median, confidence intervals) to produce a reliable throughput estimate.

### High-Level Flow

```
1. Verify vCenter credentials and privileges
2. Discover available datastores from inventory
3. Select datastore pairs to benchmark
4. For each pair:
   a. Create a temporary disk on the source datastore
   b. Fill the disk with random data using a temporary Alpine Linux VM
   c. Copy the disk from source to target (N iterations)
   d. Measure wall-clock time for each copy
   e. Clean up all temporary resources
5. Compute throughput statistics and time estimates
```

---

## Important: vCenter Resources Created

{{% alert title="Warning" color="warning" %}}
The forecaster creates temporary virtual machines and virtual disks in your vCenter environment. While all resources are cleaned up automatically after benchmarking, vCenter administrators should be aware of this activity.
{{% /alert %}}

### Resources Created Per Datastore Pair

| Resource | Location | Purpose | Lifetime |
|----------|----------|---------|----------|
| **Filler VM** | vCenter inventory | Boots Alpine Linux to fill benchmark disk with random data | ~minutes; destroyed after disk fill completes |
| **Alpine boot disk** | Source datastore | 256 MB thin VMDK for the filler VM OS | Deleted after pair completes |
| **Seed ISO** | Source datastore | Cloud-init configuration for the filler VM | Deleted after pair completes |
| **Benchmark disk** | Source datastore | Thin VMDK (user-specified size, default 10 GB) filled with random data | Deleted after pair completes |
| **Clone disk** | Target datastore | Copy of benchmark disk created during each iteration | Deleted after each iteration |
| **Directories** | Source and target datastores | `forecaster-*` directories to hold temporary files | Deleted after pair completes |

### Filler VM Specification

The temporary VM used to fill the benchmark disk:

- **Name**: `forecaster-filler-{timestamp}`
- **OS**: Alpine Linux (minimal, ~256 MB)
- **Resources**: 1 vCPU, 256 MB RAM
- **Behavior**: Boots, fills the benchmark disk with random data via `dd`, then powers off automatically
- **No network access**: The VM does not require or use network connectivity

### Cleanup Guarantees

- All resources are cleaned up automatically when a benchmark pair completes (success or failure)
- If the agent is terminated mid-benchmark, some temporary files or directories may remain on the datastores and require manual cleanup
- Temporary resource names are prefixed with `forecaster-` or `filler-image-` for easy identification
- The filler VM is always destroyed, even if the benchmark encounters errors

---

## Required vSphere Privileges

The vCenter credentials used for forecasting must have the following privileges:

| Privilege | Why |
|-----------|-----|
| `Datastore.AllocateSpace` | Create benchmark disks and directories |
| `Datastore.Browse` | List datastore contents |
| `Datastore.DeleteFile` | Clean up temporary files and directories |
| `Datastore.FileManagement` | Upload filler image and seed ISO |
| `VirtualMachine.Inventory.Create` | Create the temporary filler VM |
| `VirtualMachine.Inventory.Delete` | Destroy the filler VM after use |
| `VirtualMachine.Provisioning.Clone` | Copy disks between datastores |
| `VirtualMachine.Interact.PowerOn` | Boot the filler VM |
| `VirtualMachine.Config.AddRemoveDevice` | Attach/detach disks to the filler VM |

The credential verification endpoint (`PUT /forecaster/credentials`) checks these privileges before benchmarking starts and reports any missing ones.

---

## API Workflow

### Step 1: Verify Credentials

Validate that the vCenter credentials have the required privileges.

```bash
curl -X PUT http://agent:3443/api/v1/forecaster/credentials \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://vcenter.example.com",
    "username": "administrator@vsphere.local",
    "password": "your-password"
  }'
```

**200 OK** — credentials are valid. **403** — missing privileges (response includes `missingPrivileges` list).

### Step 2: List Datastores

Retrieve the datastores discovered from the environment inventory.

```bash
curl -X POST http://agent:3443/api/v1/forecaster/datastores
```

Returns a list of datastores with their type, capacity, vendor, and offload capabilities.

### Step 3: Check Pair Capabilities (Optional)

Check what storage offload capabilities are available for specific datastore pairs.

```bash
curl -X POST http://agent:3443/api/v1/forecaster/capabilities \
  -H "Content-Type: application/json" \
  -d '{
    "pairs": [
      {
        "name": "local-to-nfs",
        "sourceDatastore": "datastore1",
        "targetDatastore": "datastore2"
      }
    ]
  }'
```

### Step 4: Start Benchmark

Start the benchmark for one or more datastore pairs.

```bash
curl -X POST http://agent:3443/api/v1/forecaster \
  -H "Content-Type: application/json" \
  -d '{
    "pairs": [
      {
        "name": "local-to-nfs",
        "sourceDatastore": "datastore1",
        "targetDatastore": "datastore2",
        "host": "esxi-01.example.com"
      }
    ],
    "diskSizeGb": 10,
    "iterations": 5,
    "concurrency": 1
  }'
```

| Parameter | Default | Description |
|-----------|---------|-------------|
| `pairs` | *(required)* | List of datastore pairs to benchmark |
| `pairs[].host` | *(auto-selected)* | Pin to a specific ESXi host (optional) |
| `diskSizeGb` | 10 | Size of the benchmark disk in GB |
| `iterations` | 5 | Number of copy iterations per pair |
| `concurrency` | 1 | Number of pairs to benchmark in parallel |

Returns **202 Accepted** with the initial status. Returns **409 Conflict** if a benchmark is already running.

### Step 5: Poll Status

Monitor benchmark progress.

```bash
curl http://agent:3443/api/v1/forecaster
```

Each pair reports its current state:

| State | Meaning |
|-------|---------|
| `pending` | Queued, not yet started |
| `preparing` | Creating and filling the benchmark disk |
| `running` | Copying disk (iterations in progress) |
| `completed` | All iterations finished |
| `error` | Failed (see `error` field) |
| `canceled` | Stopped by user |

During `preparing`, `prepBytesTotal` and `prepBytesUploaded` track the disk fill progress.
During `running`, `completedRuns` and `totalRuns` track iteration progress.

### Step 6: View Results

Get benchmark run data.

```bash
curl "http://agent:3443/api/v1/forecaster/runs?pairName=local-to-nfs"
```

Get computed statistics and time estimates.

```bash
curl "http://agent:3443/api/v1/forecaster/stats?pairName=local-to-nfs"
```

The stats response includes mean/median/min/max throughput, standard deviation, 95% confidence interval, and estimated migration time per 1 TB (best case, expected, worst case).

### Canceling a Benchmark

Cancel all running pairs:

```bash
curl -X DELETE http://agent:3443/api/v1/forecaster
```

Cancel a single pair:

```bash
curl -X DELETE http://agent:3443/api/v1/forecaster/pairs/local-to-nfs
```

Canceling stops the active benchmark. Resources are cleaned up before the operation completes.

---

## Understanding Results

### Throughput Statistics

After a benchmark completes, the stats endpoint provides:

| Metric | Description |
|--------|-------------|
| `meanMbps` | Average throughput across all successful iterations |
| `medianMbps` | Middle value (less affected by outliers) |
| `minMbps` / `maxMbps` | Range of observed throughput |
| `stddevMbps` | Standard deviation (consistency measure) |
| `ci95LowerMbps` / `ci95UpperMbps` | 95% confidence interval for true throughput |

### Time Estimates

The `estimatePer1TB` field provides migration time forecasts for 1 TB of data:

| Estimate | Based On |
|----------|----------|
| `bestCase` | Upper bound of 95% confidence interval |
| `expected` | Median throughput |
| `worstCase` | Lower bound of 95% confidence interval |

Scale these estimates linearly for your actual data volume.

---

## Tips

- **Disk size**: Larger benchmark disks produce more realistic results but take longer to prepare. 10 GB is a good default for quick estimates.
- **Iterations**: More iterations improve statistical confidence. 5 is a reasonable default; use 10+ for production planning.
- **Host pinning**: If your migration will use a specific ESXi host, pin the benchmark to that host for more accurate results.
- **Off-peak testing**: Run benchmarks during representative load conditions to get realistic throughput numbers.
- **Multiple pairs**: If migrating across different storage backends, benchmark each unique source-target combination separately.
