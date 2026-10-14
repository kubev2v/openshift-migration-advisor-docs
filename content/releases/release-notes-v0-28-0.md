---
title: "release notes v0.28.0"
linkTitle: "release notes v0.28.0"
date: 2026-10-14
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.28.0`

Compare: `v0.27.0` → `v0.28.0`

## Appliance changes

### Features
- Added a new inventory field indicating whether vSAN snapshots are supported on each datastore
- Added standalone RVTools container image with support for Mac (ARM64 and AMD64 architectures)

### API changes (not yet available in the UI)
- Added collection of VM annotations and descriptions from RVTools data

### Fixes
- Fixed PNG exports to always use light mode regardless of the user's dark mode setting

## Console changes

### Features
- Added a form for viewing additional vCenter cluster details within assessments

### API changes (not yet available in the UI)
- Added support for multiple clusters in the complexity estimator, enabling cross-cluster aggregation
- Added inventory aggregation to combine multiple inventory sources into a unified model

### Fixes
- Fixed PDF export incorrectly including the "Shared disks" section when that view is disabled
- Fixed cluster sizing recommendations missing from the assessment PDF export
