---
title: "What Happens to Your Data? Understanding Our Aggregated Reporting Process"
linkTitle: "Aggregated Data Report"
description: "A comprehensive guide to the inventory data collected by Migration Advisor and what each field means for your migration planning."
---

The Migration Advisor tool collects data about your VMware environment to help you plan your migration to OpenShift Virtualization. This document describes all the data fields included in the aggregated inventory report.

Applies to: V0.4.0  
Last update (dd-mm-yyyy): 02-02-2026

The data fields and structure described in this document may vary between releases. 
New fields may be added and deprecated fields may be removed based on the version of the Migration Advisor tool.

## Report Structure Overview

The inventory report is organized hierarchically:

```
Inventory
├── vcenter_id          # Unique identifier for the vCenter
├── vcenter             # vCenter-level aggregated data
└── clusters            # Map of cluster names to their inventory data
    └── [cluster_name]
        ├── vms         # Virtual machine statistics
        └── infra       # Infrastructure data
```

---

## Virtual Machine Data

The `vms` section contains statistics about all virtual machines discovered in your environment.

### VM Counts

| Field | Description |
|-------|-------------|
| `total` | Total number of virtual machines discovered |
| `totalMigratable` | Number of VMs that can be migrated without issues |
| `totalMigratableWithWarnings` | Number of VMs that can be migrated but have warnings to address |

### Resource Breakdown Fields

For each major resource (CPU, RAM, Disk), the report provides a detailed breakdown:

#### CPU Cores

| Field | Description |
|-------|-------------|
| `total` | Total vCPU cores allocated across all VMs |
| `totalForMigratable` | vCPU cores for VMs that can be migrated |
| `totalForMigratableWithWarnings` | vCPU cores for VMs migratable with warnings |
| `totalForNotMigratable` | vCPU cores for VMs that cannot be migrated |

#### RAM

| Field | Description |
|-------|-------------|
| `total` | Total RAM (GB) allocated across all VMs |
| `totalForMigratable` | RAM (GB) for migratable VMs |
| `totalForMigratableWithWarnings` | RAM (GB) for VMs migratable with warnings |
| `totalForNotMigratable` | RAM (GB) for non-migratable VMs |

#### Disk Storage

| Field | Description |
|-------|-------------|
| `total` | Total disk storage (GB) across all VMs |
| `totalForMigratable` | Disk storage (GB) for migratable VMs |
| `totalForMigratableWithWarnings` | Disk storage (GB) for VMs migratable with warnings |
| `totalForNotMigratable` | Disk storage (GB) for non-migratable VMs |

#### Disk Count

| Field | Description |
|-------|-------------|
| `total` | Total number of virtual disks across all VMs |
| `totalForMigratable` | Disk count for migratable VMs |
| `totalForMigratableWithWarnings` | Disk count for VMs migratable with warnings |
| `totalForNotMigratable` | Disk count for non-migratable VMs |

### Distribution Metrics

These fields help you understand how your VMs are distributed across different resource tiers:

#### CPU Tier Distribution

Distribution of VMs across CPU tier buckets:
- `0-4` vCPUs
- `5-8` vCPUs
- `9-16` vCPUs
- `17-32` vCPUs
- `32+` vCPUs

#### Memory Tier Distribution

Distribution of VMs across memory tier buckets:
- `0-4` GB
- `5-16` GB
- `17-32` GB
- `33-64` GB
- `65-128` GB
- `129-256` GB
- `256+` GB

#### NIC Count Distribution

Distribution of VMs by network interface count:
- `0` NICs
- `1` NIC
- `2` NICs
- `3` NICs
- `4+` NICs

### Disk Information

#### Disk Size Tiers

For each disk size tier, the report provides:

| Field | Description |
|-------|-------------|
| `totalSizeTB` | Total disk size in TB for this tier |
| `vmCount` | Number of VMs in this tier |

#### Disk Types

For each disk type (e.g., thin, thick, RDM), the report provides:

| Field | Description |
|-------|-------------|
| `vmCount` | Number of VMs with at least one disk of this type |
| `totalSizeTB` | Total disk size in TB for this disk type |

### Power States

A breakdown of VMs by their power state.

### Operating System Information

For each detected operating system, the report provides:

| Field | Description |
|-------|-------------|
| `count` | Number of VMs running this OS |
| `supported` | Whether the OS is supported for migration by MTV |
| `upgradeRecommendation` | Recommended OS upgrade path for unsupported operating systems that can be upgraded to a supported version |

> **Note:** The "supported" / "unsupported" OS classification is based on [virt-v2v](https://access.redhat.com/articles/1351473), the conversion tool that MTV (Migration Toolkit for Virtualization) uses under the hood to migrate VMs to KVM for OpenShift Virtualization. An OS marked as "supported" means it has been verified and is officially supported for conversion by virt-v2v. An "unsupported" OS does not necessarily mean the migration will fail -- it means the OS has not been verified by Red Hat and will not have official support from Red Hat experts if issues arise. In many cases, unsupported OS conversions may work fine. For the full list of supported guest operating systems, see [Converting virtual machines from other hypervisors to KVM with virt-v2v](https://access.redhat.com/articles/1351473).

### Migration Issues

#### Not Migratable Reasons

A list of issues that prevent VMs from being migrated:

| Field | Description |
|-------|-------------|
| `id` | Unique identifier for the issue type |
| `label` | Human-readable description of the issue |
| `assessment` | Assessment category (e.g., "error") |
| `count` | Number of VMs affected by this issue |

**Common reasons include:**
- Unsupported disk types (RDM, shared VMDK)
- Unsupported guest operating systems
- VMs with snapshots
- VMs with USB devices attached
- VMs with NVRAM encryption

#### Migration Warnings

A list of issues that don't block migration but should be addressed:

| Field | Description |
|-------|-------------|
| `id` | Unique identifier for the warning type |
| `label` | Human-readable description of the warning |
| `assessment` | Assessment category (e.g., "warning") |
| `count` | Number of VMs affected by this warning |

**Common warnings include:**
- Changed Block Tracking (CBT) not enabled
- VMware Tools not installed or outdated
- VMs with more than 4 NICs

---

## Infrastructure Data

The `infra` section contains information about the physical infrastructure supporting your VMs.

### Summary Counts

| Field | Description |
|-------|-------------|
| `totalHosts` | Total number of ESXi hosts |
| `totalDatacenters` | Number of vSphere datacenters |
| `clustersPerDatacenter` | Cluster count per datacenter |

### Overcommitment Ratios

| Field | Description |
|-------|-------------|
| `cpuOverCommitment` | CPU overcommitment ratio (allocated vCPUs ÷ physical cores) |
| `memoryOverCommitment` | Memory overcommitment ratio (allocated memory ÷ physical memory) |

These ratios help you understand how heavily your current infrastructure is utilized and plan appropriate sizing for your OpenShift cluster.

### Host Information

For each ESXi host:

| Field | Description |
|-------|-------------|
| `id` | Unique identifier for the host |
| `vendor` | Hardware vendor (e.g., Dell, HPE, Cisco) |
| `model` | Server model |
| `cpuCores` | Number of physical CPU cores |
| `cpuSockets` | Number of CPU sockets |
| `memoryMB` | Total host memory in MB |

### Host Power States

Breakdown of hosts by power state:
- `poweredOn`
- `standby`
- `maintenance`

### Network Information

For each network in your environment:

| Field | Description |
|-------|-------------|
| `name` | Network name |
| `type` | Network type: `standard`, `distributed`, `dvswitch`, or `unsupported` |
| `vlanId` | VLAN identifier |
| `dvswitch` | Name of the distributed vSwitch (if applicable) |
| `vmsCount` | Number of VMs connected to this network |

### Datastore Information

For each datastore:

| Field | Description |
|-------|-------------|
| `type` | Storage type (VMFS, NFS, vSAN, etc.) |
| `totalCapacityGB` | Total capacity in GB |
| `freeCapacityGB` | Available free space in GB |
| `vendor` | Storage vendor |
| `model` | Storage model |
| `diskId` | Disk/LUN identifier |
| `protocolType` | Storage protocol (FC, iSCSI, NFS, etc.) |
| `hardwareAcceleratedMove` | Whether VAAI/XCOPY is supported |
| `hostId` | Identifier of the host where this datastore is attached |

---

## Data Report Generation

The data report can be generated through two methods:

### 1. Discovery Agent (OVA installation in the VSphare environment)

When using the Discovery Agent:
- Data is collected directly from vCenter APIs
- Provides the most accurate and complete information
- Updates automatically as your environment changes
- Requires deploying the OVA appliance to your vCenter

### 2. RVTools Upload

When uploading an RVTools export:
- Data is parsed from the Excel file
- Quick assessment without deploying any agents
- Data accuracy depends on when the RVTools export was generated
- Some fields may be unavailable depending on RVTools configuration

---
