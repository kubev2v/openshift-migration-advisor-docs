---
title: "release notes v0.13.6"
linkTitle: "release notes v0.13.6"
weight: 2
type: docs
slug: "release-notes-v0-13-6"
---

# Migration Planner — release notes — `v0.13.6`

Compare: `v0.13.5` → `v0.13.6`

## Enhancements

- **Applications Detection (Technology Preview)** — You can now see which applications are running on your virtual machines. A new Applications tab in the assessment report lets you search and filter by application name or VM, and drill down into which VMs are running each application. This feature is currently in Technology Preview.
- **Standalone Cluster Sizing Tool** — A new Tools tab provides an independent Cluster Sizing Tool. You can calculate target cluster requirements from workload totals, cluster mode, and system settings without needing an active assessment.
- **Migration Complexity Info** — A new help popover in the migration complexity section explains how complexity tiers are calculated, with color-coded badges and tier descriptions.
- **Report Chart Drill-Down** — Clicking a chart slice or legend entry in assessment reports (memory, disk, cluster, network) now opens the Virtual Machines tab with the matching filter applied, making it easier to explore specific VM segments.
- **Improved Groups Column** — The Groups column in the VMs table now displays groups as a vertical list with direct links to each group's detail page, with a "Show more" toggle when there are many groups.

## Bug Fixes

- **Cancel Deep Inspection Per VM** — Canceling a deep inspection on a single VM no longer stops inspections running on other VMs.
- **Group Report Issue Counts** — The "With issues" breakdown in group reports now correctly shows issue counts scoped to the selected group, rather than the entire inventory.
- **VM Count Updates After Exclusion** — Assessment report VM counts now update immediately after excluding or including a VM, without waiting for the next server refresh.
- **Source URL Validation** — Fixed an issue where certain invalid URL formats were incorrectly accepted when configuring a migration source.
- **Group Membership Error** — You now get a clear error message when trying to add a source that already belongs to another group.
