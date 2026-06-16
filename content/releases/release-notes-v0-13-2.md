---
title: "release notes v0.13.2"
linkTitle: "release notes v0.13.2"
weight: 6
type: docs
---

# Migration Planner — release notes — `v0.13.2`

Compare: `v0.13.1` → `v0.13.2`

## Enhancements

- **Used Resources Column** — The agent UI now displays a "Used Resources" column in the VMs table, showing resource utilization for each virtual machine.
- **Storage Offload Estimator (Technology Preview)** — A new Storage Offload estimator tab is available in the agent UI, marked with a Technology Preview badge, to help evaluate storage migration strategies.
- **Cluster Sizing and Utilization Info** — The agent UI now shows cluster sizing information along with VM utilization data, giving you a more complete picture of your infrastructure.
- **Cost Estimation Environment Details** — The Cost Estimation tab now includes customer environment information for more accurate cost analysis.
- **Group Details Navigation** — A back button is now available on the group details page for easier navigation.
- **OVA Assessment Guidance** — Assessment reports now include guidance about viewing more detailed results using the discovery OVA.
- **Shared Assessment Attribution** — The assessment table now shows "Shared by" with the customer name for shared assessments.

## Bug Fixes

- **Discovery Agent Instructions Link** — Fixed an incorrect "Read more" URL in the discovery agent instructions.
- **Deep Inspection Reliability** — Fixed issues with deep inspection processing that could cause unexpected behavior.
- **Cost Estimation Empty Values** — Removed empty values from the Cost Estimation tab display.
- **vCenter URL Handling** — Fixed a 400 Bad Request error that occurred when the vCenter URL was missing the `/sdk` suffix.
