---
title: "release notes v0.26.0"
linkTitle: "release notes v0.26.0"
date: 2026-10-01
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.26.0`

Compare: `v0.25.0` → `v0.26.0`

## Appliance changes

### Features
- Added PDF, PNG, and HTML export options for assessment report charts and infographics

### Fixes
- Assessment report header and Virtual Machines tab now correctly scope to the selected cluster
- Agent now requires a data folder argument, preventing credential failures on restart
- Cleared stale "New report failed" error message after successful data collection on vCenter reconnect
- Fixed label length validation to show the error message directly in the add/manage labels modal

## Console changes

### Features
- Added all-cluster support in migration recommendations — architecture sizing, cluster requirements, and migration time estimation now available for all vSphere clusters in a single view

### API changes (not yet available in the UI)
- Added storage protocol information to the inventory API

### Fixes
- Disabled assessment-created email notifications for administrators and partners creating their own assessments
- Authorization records are now properly cleaned up when a group is deleted
- Added sorting support for the Data Center column
- Group detail header VM count now updates correctly after removing VMs from a group
- Separated file upload from JSON inventory upload into its own API endpoint, fixing the published TypeScript SDK build
- Fixed OVA download event tracking to use correct identifiers
- Fixed missing partner names in analytics events
