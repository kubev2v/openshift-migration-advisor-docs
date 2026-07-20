---
title: "release notes v0.18.0"
linkTitle: "release notes v0.18.0"
date: 2026-07-15
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.18.0`

Compare: `v0.17.0` → `v0.18.0`

## Appliance changes

### Features
- Replaced table filter dropdowns with attribute-value filters for a more consistent and intuitive filtering experience across VM tables, groups, and applications
- Improved Storage Offload Estimator reliability by preventing duplicate result loads and ensuring the Start Over flow completes cleanly
- Removed deprecated cluster rightsizing API endpoints

### API changes (not yet available in the UI)
- Added batch VM exclusion API endpoint for excluding or including multiple VMs in a single operation, significantly improving performance for large selections

### Fixes
- Fixed empty VM group sync causing a permanent loss of console connectivity until agent restart
- Fixed capabilities and privilege detection failing on vCenter environments with multiple datacenters
- Disabled action menus for VM groups containing no VMs

## Console changes

### Features
- Replaced table filter dropdowns with attribute-value filters for a more consistent and intuitive filtering experience across assessments and sources tables
- Added separate base URL configuration for cost estimation API endpoints via 3scale routing

### API changes (not yet available in the UI)
- Added OS support tier classification to the inventory API, categorizing each guest OS as certified, vendor supported, community supported, or requiring special handling
- Added issues breakdown by severity category to the inventory API, providing per-category VM counts in a single call

### Fixes
- Fixed groups selector and Discovery VM status not loading correctly on first visit to the report page
- Fixed agent version popover appearing inconsistently for environments created with manually uploaded inventory
- Fixed standalone sizing tool incorrectly applying overcommitment settings to compact and SNO cluster modes
