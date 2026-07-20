---
title: "release notes v0.13.1"
linkTitle: "release notes v0.13.1"
date: 2026-05-04
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.13.1`

Compare: `v0.13.0` → `v0.13.1`

## Enhancements

- **Cost Estimation Tab Enabled** — The Cost Estimation tab in assessment reports is now fully enabled and accessible, providing migration cost analysis alongside your assessment data.
- **Migration Benchmarking (Agent UI)** — A new benchmarking interface in the discovery agent lets you run and view migration performance benchmarks for your VMs, helping you estimate actual migration times.
- **Assessment Sharing Status** — The assessment view now displays "Shared by" or "Shared with" information, making it clear who initiated the sharing and who has access.

## Bug Fixes

- **Estimation by Complexity** — Fixed an issue where estimation calculations by complexity produced incorrect results.
- **Partner Access Revocation** — Partner access to shared assessments is now correctly revoked when a customer leaves a group.
