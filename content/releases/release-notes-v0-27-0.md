---
title: "release notes v0.27.0"
linkTitle: "release notes v0.27.0"
date: 2026-10-07
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.27.0`

Compare: `v0.26.0` → `v0.27.0`

## Appliance changes

### Features
- Added PDF, PNG, and HTML export options for assessment report charts and infographics
- Added virtual disk count to the VM data export

### Fixes
- Fixed assessment report header and Virtual Machines tab not responding to cluster dropdown selection
- Fixed error message display when adding a label that exceeds the maximum character length

## Console changes

### Features
- Added all-cluster architecture sizing — migration recommendations, cluster requirements, and migration time estimates are now available across all vSphere clusters in a single view
- Added PDF, PNG, and HTML export options for assessment report charts and infographics
- Added ability to revoke a previously shared assessment with a partner
- Added search functionality to the partners list for faster partner lookup

### API changes (not yet available in the UI)
- Added storage protocol information to the inventory API

### Fixes
- Fixed TypeScript API client build failure by separating file upload from JSON inventory upload into its own API operation
