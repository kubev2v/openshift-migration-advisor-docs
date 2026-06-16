---
title: "release notes v0.13.0"
linkTitle: "release notes v0.13.0"
weight: 8
type: docs
---

# Migration Planner — release notes — `v0.13.0`

Compare: `v0.12.0` → `v0.13.0`

## Enhancements

- **Assessment Sharing** — You can now share assessments with partners. The assessment table displays sharing status, and a confirmation modal guides you through the sharing process.
- **Cost Estimation Tab** — A new Cost Estimation tab is available in assessment reports, providing cost analysis for your migration planning.
- **Customer List for Partners** — Partners can now view a list of their associated customers directly in the partner view.
- **Cluster Sizing PDF Export** — You can now persist cluster sizing inputs and export cluster recommendations to PDF for offline review and stakeholder sharing.
- **Example Report Improvements** — The example report now includes a cluster recommendations section, giving new users a better preview of the full assessment capabilities.
- **Partner Features Generally Available** — Partner management features are now visible and accessible to all users without requiring a feature flag.

## Bug Fixes

- **Deep Inspection Reset** — Resetting deep inspection configuration no longer fails when no VMs are selected.
- **Deep Inspection Button State** — The "Run deep inspection" button is no longer stuck in a disabled state during an active inspection run, allowing you to select additional VMs.
- **Deep Inspection Status** — Deep inspection status no longer hangs on "Running" in the agent UI after the backend has completed processing.
- **Browser Crash on Navigation** — Fixed a crash in Chrome that could occur during certain navigation patterns.
- **Assessment Creation Errors** — Backend validation errors are now correctly surfaced when creating assessments, and stale error messages are properly cleared.
- **Environment Network Editing** — Edit environment network and proxy settings now apply correctly.
- **Partner Contact Form Validation** — Added input validation to the partner contact form with clear error messages for invalid entries.
- **File Selection Error Clearing** — Backend errors are now properly cleared when selecting a valid file in the Create Assessment modal.
