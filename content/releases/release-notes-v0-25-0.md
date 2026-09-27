---
title: "release notes v0.25.0"
linkTitle: "release notes v0.25.0"
date: 2026-09-23
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.25.0`

Compare: `v0.24.0` → `v0.25.0`

## Appliance changes

### Features
- Added ability to delete collected data and remove credentials when disconnecting from vCenter, with options to keep or remove previously collected data
- Added group-based filtering on the Applications tab, scoping displayed applications to the VMs in the selected group
- Added infrastructure summary and power-state breakdown cards to the assessment report for both all-clusters and per-cluster views

### API changes (not yet available in the UI)
- Added sorting support for the Data Center column in the VM inventory table

### Fixes
- Fixed inability to re-run data collection after deleting collected data, which left the appliance unable to collect until manual intervention
- Fixed "Latest run" status not refreshing when a collection run was already in progress before the page loaded
- Fixed "Create assessment report" button remaining clickable after the first click, preventing accidental duplicate submissions

## Console changes

### Features
- Added infrastructure summary and power-state breakdown cards to the assessment report for both all-clusters and per-cluster views
- Simplified assessment table navigation by making the assessment name link directly to the report page, removing the separate report column

### Fixes
- Fixed server startup failure when admin group members already existed in the database, which prevented the console from starting after a restart

### API changes (not yet available in the UI)
- Added standalone ESXi host detection to the inventory infrastructure model, surfacing whether standalone hosts were found during discovery
