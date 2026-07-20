---
title: "release notes v0.13.4"
linkTitle: "release notes v0.13.4"
date: 2026-05-28
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.13.4`

Compare: `v0.13.3` → `v0.13.4`

## Enhancements

- **Column Management Modal** — A new column management modal replaces the dropdown for configuring visible columns in tables, providing a cleaner and more intuitive column selection experience.
- **VM Labels** — You can now add, edit, and manage labels on individual VMs or in batch. Labels can be used to filter VMs in tables and when creating groups.
- **Exclude/Include VMs from Reports** — You can now exclude or include specific VMs directly from the agent UI, controlling which VMs appear in assessment reports and recommendations.
- **Standalone Cluster Sizing** — A new standalone cluster sizing capability lets you calculate target cluster requirements from workload totals without needing an active assessment.
- **VM Filter Options** — A dedicated filter options endpoint provides faster, more efficient filtering in VM tables with large inventories.

## Bug Fixes

- **Long Assessment Name Truncation** — Long assessment names are now properly truncated in the UI instead of overflowing.
- **Group Description Persistence** — Saving a group with an empty description no longer fails silently.
- **Resource Usage Precision** — Resource usage values now display with decimal point precision for more accurate readings.
- **Deep Inspection Column Sorting** — Deep Inspection column sorting now works correctly during active inspections.
- **Re-Run Benchmark Button** — The "Re-run benchmark" button is now shown consistently across all benchmark result states.
- **Benchmark Cancellation Message** — Canceling a benchmark now shows a clear "canceled" message instead of an error.
- **Deep Inspection Issue Count** — The Deep Inspection column no longer incorrectly shows "0 issues" when an inspection has failed.
- **Datastore Pair Statistics** — Selecting a datastore pair from the results list now correctly displays that pair's statistics.
