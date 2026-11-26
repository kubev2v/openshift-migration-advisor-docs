---
title: "release notes v0.33.0"
linkTitle: "release notes v0.33.0"
date: 2026-11-26
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.33.0`

Compare: `v0.32.0` → `v0.33.0`

## Appliance changes

### Features
- Added migration complexity and time estimation to the offline analyzer recommendations
- Added heuristic application detection with confidence ratings based on vApp product data
- Enhanced data collection with host hardware details and storage export metadata
- Added support for managing multiple RVTools inventories per collection, including uploading additional files and deleting individual inventories
- Added vCenter selector for multi-vCenter inventory analysis in the standalone analyzer
- Increased maximum RVTools file upload limit from 10 to 50
- Consolidated the appliance UI by removing the legacy RVTools mode

### API changes (not yet available in the UI)
- Exposed /appliance endpoint on the agent for appliance metadata and status queries
- Added appliance image download for disconnected users via the console

### Fixes
- Fixed VM connected to multiple networks being counted multiple times in the Network overview
- Improved RVTools file validation error messages to be clearer and more actionable
- Fixed category lookup timeout causing missing VM tags during data collection
- Fixed analyzer API omitting existing VM and application metadata
- Fixed incorrect icon for powered-on VM power status

## Console changes

### Features
- Redesigned the Discovery Appliances experience with new table layout, creation modal, onboarding integration, and smart redirect after assessment creation
- Added the ability to rename assessments
- Increased maximum RVTools file upload limit from 10 to 50

### API changes (not yet available in the UI)
- Exposed assessment-list filters by source type
- Added automatic appliance image upgrade with minimum version enforcement and health-gated rollback
- Added appliance image download for disconnected users

### Fixes
- Fixed breadcrumb labels displaying lowercase route segments instead of matching tab names
- Fixed vCenter filter incorrectly including the Group filter
- Fixed wrong links redirect on the Empty Assessment page
- Fixed older assessments showing zero inventory counts despite having populated reports
- Fixed incorrect error message when renaming an assessment to a name already in use
- Fixed deleting a partner group shared with an assessment causing an HTTP 500 error
- Fixed UI version name always showing "unknown"
