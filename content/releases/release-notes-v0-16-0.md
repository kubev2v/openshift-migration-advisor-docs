---
title: "release notes v0.16.0"
linkTitle: "release notes v0.16.0"
weight: 2
type: docs
---

# Migration Planner — release notes — `v0.16.0`

Compare: `v0.15.0` → `v0.16.0`

### Enhancements

- **Updated agent interface branding.** The discovery agent interface now features the Red Hat OpenShift logo and an improved navigation menu, aligning with Red Hat branding standards.

- **Credentials are now optional for migration source discovery.** You can now start a discovery without providing credentials upfront. If credentials were previously saved, the agent reuses them automatically, simplifying repeated discovery workflows.

### Bug Fixes

- **Compact mode setting is now correctly preserved.** Fixed an issue where selecting compact mode in cluster requirements was not being saved, which could lead to incorrect sizing recommendations.

- **Enter key now works in the group creation dialog.** You can now press Enter to submit the form when creating a new group in the agent interface, instead of having to click the submit button.

- **Corrected "VMWare" to "VMware" throughout the interface.** Fixed the product name spelling to match the correct branding.
