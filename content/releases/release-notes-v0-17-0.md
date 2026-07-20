---
title: "release notes v0.17.0"
linkTitle: "release notes v0.17.0"
date: 2026-07-08
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.17.0`

Compare: `v0.16.0` → `v0.17.0`

## OpenShift Migration Appliance

### Features
- Added CSV export for VM inventory data — download a ZIP of CSVs covering VMs, hosts, clusters, datastores, network, storage forecast, applications, and groups
- Added export button to the agent UI report page for downloading inventory data
- Centralized vCenter credential management — credentials are entered once and reused across storage offload and deep inspection workflows, removing repeated password prompts
- Added per-NIC IPv4 and IPv6 addresses in the VM details network view, replacing the single VM-level IP address previously shown for all NICs
- Added the ability to cancel in-flight storage offload benchmarks, with per-pair and global cancel actions
- "Start over" in the storage offload estimator now properly clears previous estimation runs on the backend, preventing cleared runs from reappearing

### Fixes
- Fixed storage offload estimator showing "Password is required" error when re-running benchmarks or adding datastore pairs
- Fixed vCenter credentials being incorrectly pre-filled when adding new datastore pairs
- Fixed group assessment report showing wrong content (full vCenter report instead of group-scoped report) after switching tabs
- Agent now returns a graceful error response instead of HTTP 500 when vCenter capabilities cannot be retrieved
- Fixed collector not accepting empty-body requests when using stored credentials

## OpenShift Migration Console

### Features
- Added group-based filtering to the assessment report — users can scope the dashboard, cluster filters, and exports to a specific VM group
- Added subset VM views to assessment pages — when groups are present, tabs appear for each group alongside the "All vSphere" view
- Updated cost estimation with new form-based inputs: Red Hat edition selector, ACM checkbox, consolidation percentage, VVS comparison column, and discount options
- Added compact mode (3 schedulable control-plane nodes, no workers) to cluster sizing recommendations
- Increased default worker node CPU overcommitment ratio to 1:8 in cluster recommendations
- Improved partner management UI with direct image upload, automatic Base64 conversion, and live preview of partner cards during creation

### Fixes
- Fixed manual inventory upload on the OVA create page not showing proper error messages, aligning behavior with the environments table
- Fixed unescaped numeric fields in HTML export causing rendering issues
- Fixed PDF report including the "Shared disks vs. No shared disks" section when there are no shared disks, matching the disabled state in the UI
- Fixed "Export Report" button misalignment on the assessment report page
- Fixed environment proxy update not clearing the noProxy value when set to null
- Fixed agent-to-console sync failing with 401 Unauthorized on group sync, preventing subsets from reaching the backend
- Fixed assessment deleted event payload to include the deletion timestamp
- Fixed Envoy routing for new agent API inventory and subset endpoints
