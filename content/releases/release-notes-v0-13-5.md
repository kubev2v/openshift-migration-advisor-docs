---
title: "release notes v0.13.5"
linkTitle: "release notes v0.13.5"
date: 2026-06-08
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.13.5`

Compare: `v0.13.4` → `v0.13.5`

## Enhancements

- **Group Management (Agent UI)** — A new group management interface in the discovery agent lets you create, view, and manage VM groups directly during discovery, with search and filtering capabilities.
- **Environment Sorting** — You can now sort the Environments list by column headers for easier navigation when managing multiple environments.
- **OVA Re-Download** — The environment modal now provides an option to re-download the discovery OVA, useful when the original download was interrupted or lost.
- **CPU and Memory Max Metrics** — The VM list now shows maximum CPU and memory utilization values alongside averages, giving better visibility into peak resource usage.

## Bug Fixes

- **RVTools Upload Progress** — Upload progress now shows immediately when creating an RVTools assessment, instead of appearing to stall before starting.
- **Source URL Validation** — Fixed an issue where certain invalid URL formats were incorrectly accepted when configuring a migration source.
- **HTML Export Charts** — Fixed numeric field handling in HTML export chart scripts that could cause rendering issues.
- **Assessment Name Tooltip** — Assessment name tooltips now work correctly when the name is a clickable link.
- **Deep Inspection Cancellation** — Cancelling a deep inspection on one VM no longer stops inspections running on other VMs.
- **Download OVA Modal** — The Download OVA modal now displays correctly during the assessment creation flow.
- **Environment List Display** — The environment list now renders correctly after generation completes.
- **VM Label Filter Logic** — The VM label filter now correctly applies OR logic when filtering by multiple labels, showing VMs that match any selected label.
- **Filter Dropdown Errors** — Fixed errors that could occur when using filter dropdowns in the agent UI.
- **Group Detail Table Alignment** — Table headers and data columns are now properly aligned in the group detail view.
- **Label Display** — Improved label display formatting and consistency in the agent UI.
