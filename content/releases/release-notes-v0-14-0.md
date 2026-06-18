---
title: "release notes v0.14.0"
linkTitle: "release notes v0.14.0"
weight: 2
type: docs
---

# Migration Planner — release notes — `v0.14.0`

Compare: `v0.13.6` → `v0.14.0`

## Enhancements

- **Cluster sizing now accounts for CPU overcommit ratios.** You can now configure the sizer with a 1:8 CPU overcommit ratio, allowing for more efficient resource allocation recommendations. Additionally, cluster utilization data is integrated into sizing calculations to provide more accurate recommendations based on actual workload patterns.
- **Cluster sizing supports larger memory configurations.** You can now configure sizing recommendations with more than 512 GB of memory per node, enabling support for larger workload requirements.
- **Rightsizing information is now included in cluster recommendations.** The cluster sizing output now displays rightsizing recommendations to help optimize resource allocation for your migrated workloads.
- **Work node size increased in sizer calculations.** The sizer now recommends larger work node configurations to better accommodate typical enterprise workload requirements.
- **VM list now supports group filtering.** You can now filter virtual machines by group in the assessment interface, making it easier to manage and review VMs organized by business unit or application.
- **New sorting and filtering options for utilization data.** The interface now supports sorting and filtering on utilization metrics, helping you identify and prioritize VMs based on resource consumption patterns.

## Bug Fixes

- **Fixed validation errors in configuration forms.** Corrected issues where validation messages were not displaying correctly and proxy configuration validation was not working as expected.
- **Fixed VM count accuracy in Assessment Reports.** VM counts in assessment reports now correctly reflect the current state after VMs have been excluded or included from the migration scope.
- **Fixed search functionality for applications.** Application name searches that were previously truncated now work correctly.
- **Fixed scrolling issue in cluster sizing tool.** Scrolling in the cluster sizing interface no longer unintentionally modifies numeric field values.
- **Fixed color inconsistencies between dark and light modes.** UI elements now display consistent colors regardless of your selected theme.
- **Fixed permission issues in standalone mode.** Resolved an issue where certain permissions were not working correctly when running Migration Advisor in standalone mode.
- **Fixed customer user access to partner groups.** Customer users can now properly access and read data from their associated partner groups.
- **Updated "Unsupported by MTV" label to "Recommended out of scope".** The terminology for VMs that should not be migrated has been clarified to better reflect that these are recommendations rather than technical limitations.
- **Fixed IP address population from vSphere.** Per-NIC IP addresses are now correctly populated from GuestNetworks data during vSphere inventory discovery.

