---
title: "Beyond the Numbers: OMA Estimations"
linkTitle: "OMA Estimations"
description: "A deep dive into the methodology behind our OMA recommendations"
---
# Migration Estimations

This document describes the estimation logic implemented in the OMA tool. It covers two main areas: **complexity estimation** (OS and disk tiers) and **time estimation** (storage migration and post-migration checks).

Applies to: V0.7.0
Last update (dd-mm-yyyy): 12-03-2026


---

## 1. Complexity Estimation

Complexity estimation provides a breakdown of how difficult a migration is expected to be, based on two independent dimensions: **OS type** and **disk size**. These scores are used for planning and prioritization; they do not directly affect time calculations.

### 1.1 Score Scale
The numeric range is 1–4, where 1 is the easiest and 4 is the most complex.

| Score | Meaning                                                  |
|-------|----------------------------------------------------------|
| 0     | OS not recognised; complexity cannot be assessed         |
| 1     | Straightforward migration, minimal intervention expected |
| 2     | Standard migration, some attention required              |
| 3     | Complex migration, more effort expected                  |
| 4     | May involve a manual intervention and special handling   |
q
- **OS scores**: 0–4 (0 = unknown)
- **Disk scores**: 1–4 (unknown does not apply to disk size)

---

### 1.2 OS Map (OS Difficulty Scores)

The OS complexity is derived by **substring matching** the VM's OS name (as reported by VMware) against the OS difficulty scores map. Matching is **case-insensitive**. If no keyword matches, the OS receives score **0 (unknown)**.

The classify OS function iterates over the map and returns the score of the first matching keyword. When multiple keys could match the same OS name, they are designed to carry the same score so iteration order does not affect the result.

#### Full OS Map

| Score | OS Family                 | Matched Versions / Notes                          |
|-------|---------------------------|---------------------------------------------------|
| **1** | Red Hat Enterprise Linux  | 6, 7, 8, 9, 10                                    |
|       | Red Hat Fedora            | all                                               |
|       | CentOS                    | 6, 7, 8, 9                                        |
|       | Oracle Linux              | 6, 7, 8, 9                                        |
|       | Rocky Linux               | 8, 9                                              |
| **2** | Red Hat Enterprise Linux  | 4, 5                                              |
|       | CentOS                    | 4, 5                                              |
|       | Oracle Linux              | 4, 5                                              |
|       | SUSE Linux Enterprise     | 12, 15                                            |
|       | Microsoft Windows Server  | 2016, 2019, 2022, 2025                           |
|       | Microsoft Windows         | 10, 11                                            |
| **3** | SUSE Linux Enterprise     | 8, 9, 10, 11                                      |
|       | SUSE openSUSE            | all                                               |
|       | AlmaLinux                 | 8, 9                                              |
|       | Ubuntu Linux              | 18.04, 20.04, 22.04, 24.04, generic               |
|       | Debian GNU/Linux          | 5–12                                              |
|       | Microsoft Windows Server  | 2000, 2003, 2008, 2008 R2, 2012, 2012 R2         |
|       | Microsoft Windows         | XP, Vista, 7, 8                                   |
|       | Oracle Solaris            | 10, 11                                            |
|       | FreeBSD                   | all                                               |
|       | VMware Photon OS          | all                                               |
|       | Amazon Linux 2            | all                                               |
|       | CoreOS Linux              | all                                               |
|       | Apple macOS               | all                                               |
| **4** | Microsoft SQL             | all (database workload)                           |
| **0** | *(any other)*             | Unknown — e.g. "Other (64-bit)", unrecognised OSes |

---

### 1.3 Disk Tiers (Disk Size Scores)

Disk complexity is derived from the user input, each tier maps to a numeric score.

| Tier Label  | Size Range (Provisioned) | Score |
|-------------|---------------------------|-------|
| 1 (0-10TB)  | ≤ 10 TB                   | 1     |
| 2 (11-20TB) | ≤ 20 TB                   | 2     |
| 3 (21-50TB) | ≤ 50 TB                   | 3     |
| 4 (>50TB)   | > 50 TB                   | 4     |

---

## 2. Time Estimation

Time estimation combines multiple **calculators**, each modelling one phase of the migration. The estimation runs all registered calculators and sums their durations to produce a total migration time.

### 2.1 Calculators Overview

| Calculator              | Phase                    | Required Params | Optional Params                                                                  |
|-------------------------|--------------------------|-----------------|----------------------------------------------------------------------------------|
| Storage Migration       | Data transfer            | Total disk in GB | Transfer rate mbps                                                               |
| Post-Migration Checks   | Post-migration troubleshooting | vm count       | troubleshoot mins per vm, number of post migration engineers, work hours per day |

---

### 2.2 Storage Migration Calculator

Estimates the time required to transfer VM storage data from the source to the target cluster over the network.

#### Assumptions

- **Transfer rate**: Default 620 Mbps (77.5 MB/s). This matches a baseline of ~110 minutes per 500 GB.
- **Data size**: Uses total provisioned disk size across all VMs in the cluster (in GB).
- **Linear transfer**: Assumes sustained throughput; no parallelism or overlap with other phases.

#### Formula

```
transferRateMBps = transferRateMbps / 8
totalMinutes = (totalDiskGB × 1024) / transferRateMBps / 60
```

Where:
- `totalDiskGB` = total disk size in gigabytes
- `1024` = MB per GB
- `60` = seconds per minute

#### Example

**Input:**
- `total_disk_gb`: 1000
- `transfer_rate_mbps`: 620 (default)

**Calculation:**
```
transferRateMBps = 620 / 8 = 77.5 MB/s
totalMinutes = (1000 × 1024) / 77.5 / 60 ≈ 220.2 minutes
```

**Output:**
- Duration: ~3h 40m
- Reason: `"1000.00 GB at 620 Mbps (110 min/500GB)"`

---

### 2.3 Post-Migration Troubleshooting Calculator

Estimates the time engineers spend on post-migration checks and troubleshooting per VM.

#### Assumptions

- **Troubleshooting time**: Default 60 minutes per VM.
- **Engineers**: Default 10 engineers working in parallel.
- **Work hours**: Default 8 hours per day (used only for the reason string, not for duration).
- **Parallelism**: Total man-minutes divided by engineer count gives wall-clock time.

#### Formula

```
totalManMins = vmCount × troubleshootMinsPerVM
realTimeMins = totalManMins / engineerCount
duration = realTimeMins minutes
```

#### Example

**Input:**
- `vm_count`: 50
- `troubleshoot_mins_per_vm`: 60 (default)
- `post_migration_engineers`: 10 (default)
- `work_hours_per_day`: 8 (default)

**Calculation:**
```
totalManMins = 50 × 60 = 3000
realTimeMins = 3000 / 10 = 300 minutes
workDays = ceil(300 / (8 × 60)) = ceil(300 / 480) = 1
```

**Output:**
- Duration: 5h 0m
- Reason: `"50 VMs @ 60.0 mins each / 10 engineers working 8 h/day for a total of 1 work days"`

---

### 2.4 Combined Example

**Input (from cluster inventory):**
- Total disk: 2000 GB
- VM count: 100
- Defaults for all optional params

**Storage Migration:**
- `(2000 × 1024) / (620/8) / 60 ≈ 440.4 min` → **~7h 20m**

**Post-Migration Checks:**
- `100 × 60 / 10 = 600 min` → **10h 0m**

**Total migration time:** ~17h 20m

