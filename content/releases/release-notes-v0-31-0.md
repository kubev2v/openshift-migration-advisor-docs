---
title: "release notes v0.31.0"
linkTitle: "release notes v0.31.0"
date: 2026-11-04
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.31.0`

Compare: `v0.30.0` → `v0.31.0`

## Appliance changes

### Features
- Added detailed storage information for VM disks, including datastore type, VMFS version, and storage protocol classification (Block, File, or Object)
- Added network adapter details for each virtual machine, including NIC count and adapter model
- The selected cluster filter in the Offline Analyzer is now preserved in the URL, allowing filtered views to be bookmarked and shared

### Fixes
- Fixed the Offline Analyzer incorrectly reporting only one vCenter when analyzing multiple RVTools files from different vCenters
- Fixed the appliance displaying a placeholder version instead of the actual release version
- Fixed the cluster filter resetting when navigating back to Virtual Machines from the Groups tab
- Improved the visibility of the Disabled status icon in the Cluster Details section

## Console changes

### Features
- Assessment reports now display the original data collection timestamp, showing when vSphere or RVTools data was collected

### Fixes
- Fixed new RVTools assessment reports appearing empty until the page was manually refreshed
- Fixed uploading an invalid or outdated inventory file being silently accepted; uploads with an unrecognized schema are now rejected with an error
- Fixed a Group filter incorrectly appearing on assessment reports created from RVTools file uploads
- Fixed the Empty Group option not appearing in the Filter by Group dropdown
