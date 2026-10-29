---
title: "release notes v0.30.0"
linkTitle: "release notes v0.30.0"
date: 2026-10-28
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.30.0`

Compare: `v0.29.0` → `v0.30.0`

## Appliance changes

### Features
- Introduced the Offline Analyzer, a standalone application for analyzing RVTools exports without connecting to vSphere
- Added support for collecting and displaying VM tags and custom attributes from vSphere and RVTools, with filtering and grouping capabilities
- Added support for uploading multiple RVTools files in standalone mode, with the ability to update or delete previously uploaded files
- Added VM process information as an export option, allowing users to include running guest processes in CSV and Excel exports

### Fixes
- Fixed deep inspection failing with a connection error by correctly supplying the vCenter certificate thumbprint
- Fixed inventory view not updating after re-uploading RVTools files, which previously required a page refresh
- Compacted the report header and VM table toolbar to reclaim vertical space

## Console changes

### Features
- Added support for manually uploading a subset inventory ZIP file for disconnected environments

### API changes (not yet available in the UI)
- Added NIOC (Network I/O Control) configuration fields to the assessment API for user-provided network data

### Fixes
- Fixed assessment creation failing when uploading certain RVTools files due to a parsing error
