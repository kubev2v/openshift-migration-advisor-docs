---
title: "release notes v0.12.0"
linkTitle: "release notes v0.12.0"
weight: 9
type: docs
---

# Migration Planner — release notes — `v0.12.0`

Compare: `v0.11.0` → `v0.12.0`

## Enhancements

- **Dark Mode Support** — Migration Advisor now fully supports dark mode, including charts, forms, assessment report PDF export, and all UI components.
- **Partner Management** — A new Partner section lets you manage partner relationships, view and respond to customer requests, and track pending partnership requests with a notification badge.
- **Groups Management** — You can now create, edit, and manage groups with full member management directly from the admin UI.
- **Color-Blind Friendly Charts** — Assessment report charts now use a color-blind friendly palette for better accessibility.
- **Granular Disk Size Tiers** — Disk size charts in assessment reports now display 8 granular tiers for more detailed storage analysis, with updated legends in both the report and example report.
- **Console Search Integration** — Migration Advisor is now discoverable through the OpenShift console search, making it easier to find the tool.
- **Agent Version Status** — The Environments table now shows more detailed agent version status options for better monitoring of discovery agents.
- **URL Rename** — The application URL has been updated from "migration-assessment" to "migration-advisor" to better reflect the product name.

## Bug Fixes

- **Network Configuration Preserved on Edit** — Existing network configuration is now correctly populated when editing an environment, preventing accidental data loss.
- **Estimation Consistency** — Time estimation and complexity estimation now use the same default parameters, ensuring consistent results across views.
- **Over-Committed Memory Default** — The default over-committed memory ratio has been changed to 1:4 for more accurate cluster sizing recommendations.
- **PDF Export in Dark Mode** — Assessment report PDF is now readable when exported in dark mode.
- **Cluster Recommendations Alignment** — Content in the cluster recommendations modal is now properly aligned.
- **Legacy RVTools Support** — RVTools files using legacy column names are now accepted during upload.
- **Cancel Job State** — Job state now resets immediately when a task is canceled, preventing stale status display.
- **Agent Report Alignment** — The agent report layout has been aligned with the SaaS report for a consistent experience.
- **OS Distribution Chart** — The OS Distribution chart now shows supported operating systems first for easier reading.
