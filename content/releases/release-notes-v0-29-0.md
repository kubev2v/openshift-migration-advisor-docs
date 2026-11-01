---
title: "release notes v0.29.0"
linkTitle: "release notes v0.29.0"
date: 2026-10-19
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.29.0`

Compare: `v0.28.0` → `v0.29.0`

## Appliance changes

### Features
- Added support for downloading individual inventory subsets for use in disconnected environments
- Added a virtual disk inventory tab to exported Excel/CSV reports

### Fixes
- Fixed VM selection persisting when switching between clusters
- Fixed Total Usage statistics showing data for the previously visited cluster instead of all clusters when viewing all vSphere clusters
- Fixed detected VMs count changing based on the selected cluster filter instead of showing the total count
- Fixed assessment report donut charts displaying gaps when all values belong to a single category

## Console changes

### Features
- Preserved original cluster IDs across the appliance and SaaS environments for consistent cluster identity

### API changes (not yet available in the UI)
- Added support for ingesting multiple RVTools files into a single assessment
- Added organization name resolution from organization IDs via IAM integration
- Added OpenAPI definitions for v2 assessment and RVTools API endpoints

### Fixes
- Fixed unnecessary whitespace padding at the bottom of dashboard metric cards
- Fixed Partner/Admin group creation preview being clipped at the screen edge
- Fixed assessment report donut charts displaying gaps when all values belong to a single category
- Fixed a regression where the PDF export included the "Shared disks" section when that view is disabled
