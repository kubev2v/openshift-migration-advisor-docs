---
title: "release notes v0.32.0"
linkTitle: "release notes v0.32.0"
date: 2026-11-11
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.32.0`

Compare: `v0.31.0` → `v0.32.0`

## Appliance changes

### API changes (not yet available in the UI)
- Added VLAN information and IP address lists to network adapter inventory for both live discovery and RVTools imports
- Added host physical NIC identity and link speed to the inventory, available in VM details and exports
- Exposed host storage adapter inventory including HBAs, WWNs, and LUN associations through the inventory API
- Added VM annotations and descriptions collection from vSphere, available in the VM details API

### Fixes
- Fixed empty Datacenters in the "All vSphere clusters" view caused by missing datacenter data during inventory import

## Console changes

### Features
- Redesigned the discovery appliance management experience with updated forms for generating and editing appliances, streamlined toolbars, redesigned action menus, a new onboarding page for first-time users, updated empty states, and a refreshed OVA download modal
- Redesigned the RVTools upload form with multi-file upload support, progress tracking, and improved error handling for invalid files
- Updated OS support tier classifications with the latest Red Hat compatibility matrix and added migration verification status indicators

### API changes (not yet available in the UI)
- Added VLAN information and IP address lists to network adapter inventory for both live discovery and RVTools imports
- Added host physical NIC identity and link speed to the inventory, available in VM details and exports
- Exposed host storage adapter inventory including HBAs, WWNs, and LUN associations through the inventory API
- Added v2 assessment and RVTools API endpoints with OpenAPI definitions
- Added ability to delete individual vCenter inventories from an assessment
- Added structured inventory model for assessment event streaming
- Cleaned up snapshots table schema and dependencies
- Decoupled the appliance image from the ISO build pipeline and corrected appliance version reporting in the service API

### Fixes
- Fixed RVTools report remaining empty after creating a second assessment until page refresh
- Improved RVTools upload alerts, error feedback, and design consistency for multi-file uploads
- Fixed empty Datacenters in the "All vSphere clusters" view caused by missing datacenter data during inventory import
