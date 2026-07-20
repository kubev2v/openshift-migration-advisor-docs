---
title: "release notes v0.15.0"
linkTitle: "release notes v0.15.0"
date: 2026-06-25
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.15.0`

Compare: `v0.14.0` → `v0.15.0`

## Enhancements

- **You can now create empty groups to organize your VMs before adding members.** This allows for better planning and organization of your migration projects before populating groups with virtual machines.
- **Groups can now be used to filter the VMs overview list.** Filter your virtual machines by group to focus on specific sets of VMs and streamline your workflow.
- **CPU usage, disk usage, and RAM usage columns now support sorting and filtering.** Identify resource-intensive VMs more quickly by sorting and filtering based on utilization metrics.
- **Migration Advisor now supports 3-node schedulable control plane configurations in compact mode.** Deploy to smaller target cluster footprints with compact cluster configurations.
- **The Application search input box has been increased in size.** Enhanced search experience with a larger input field for easier searching.
- **You can now create and edit groups by pressing the Enter key.** Faster workflow with keyboard shortcuts for group operations.
- **Backend error messages are now displayed during member creation failures.** Specific error messages help you resolve issues more quickly when adding members to groups.
- **The Storage Offload Estimator has been redesigned with a more modular interface.** Improved usability with a reorganized, more intuitive interface.

## Bug Fixes

- **Fixed an issue where the Migration Status graph showed incorrect Warning and Information counts.** The graph now accurately displays issue counts for different severity levels.
- **VMs with issues are now correctly excluded from the issues count in the Migration Status graph.** Issue count accuracy has been improved to properly exclude VMs with existing issues.
- **Fixed cache invalidation after group operations.** The UI now displays up-to-date information immediately after group operations complete.
- **Improved validation error messages for standalone cluster sizing.** Error messages now provide clearer guidance when configuring standalone cluster sizing.
- **Fixed an issue where the Proxy URL field was incorrectly marked as optional when No Proxy Domains were specified.** Proxy configuration validation now correctly requires the Proxy URL when No Proxy Domains are provided.
- **Fixed an issue where the download modal did not appear after updating OVA configuration.** The download modal now appears correctly after OVA configuration updates.
- **Fixed hostname validation to ensure compatibility with internal queue naming requirements.** Hostname sanitization now properly validates hostnames according to system requirements.


