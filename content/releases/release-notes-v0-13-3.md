---
title: "release notes v0.13.3"
linkTitle: "release notes v0.13.3"
date: 2026-05-18
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.13.3`

Compare: `v0.13.2` → `v0.13.3`

## Enhancements

- **Separate Example Reports** — OVA and RVTools assessments now have distinct example reports with a tabbed layout, making it easier to understand the expected output for each assessment type.
- **VM Exclusion** — You can now exclude VMs from the migration list so they are not included in reports and recommendations. Excluded VMs are filtered out of inventory generation automatically.
- **Split Resource Columns** — Used resources in the VMs table are now split into separate CPU, Memory, and Storage columns, providing more granular visibility into VM resource utilization.
- **Simplified Deep Inspection Credentials** — The deep inspection credentials flow has been simplified, reducing the steps needed to configure and run deep inspections.

## Bug Fixes

- **Upload Hang at 50 MB** — Fixed an issue where RVTools file uploads would hang at 20% progress when the file was near the 50 MB limit.
- **Standardized Cluster Terminology** — "Cluster" terminology is now consistent throughout the UI, clearly distinguishing between vSphere source clusters and OpenShift target clusters.
- **Migration Preferences State** — Migration preferences state is no longer incorrectly synchronized across unrelated tabs, preventing unexpected changes.
- **Popover Display in Light Mode** — Fixed assessment table popovers appearing black in light mode.
- **Environments Table Menu** — Fixed vertical kebab menu misalignment in the Environments table.
- **Agent Version Status Color** — The "Outdated" agent version status now displays in the correct text color.
- **Non-Migratable VM Colors** — Changed the indicator color for non-supported OS and non-migratable VMs from red to yellow, reducing unnecessary alarm.
- **Cluster Dropdown Ordering** — Cluster dropdown entries are now displayed in the correct order.
- **Data Sharing Modal** — Improved the data sharing modal with a warning icon and clearer checkbox text.
- **Deep Inspection Status** — Fixed deep inspection status getting stuck on "Running" after the backend completes, and now shows "N/A" instead of a 0% progress bar when not applicable.
- **Deep Inspection Technology Preview** — Added a Technology Preview flag to the deep inspector modal to set correct expectations.
- **IPv4 Validation Messages** — IPv4 validation errors now display user-friendly messages instead of raw validation output.
- **OVA Example Report** — Removed the "View recommendation" button from the OVA example report where it was not applicable.
