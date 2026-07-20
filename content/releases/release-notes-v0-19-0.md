---
title: "OpenShift Migration Advisor — release notes — v0.19.0"
linkTitle: "release notes v0.19.0"
weight: 2
type: docs
---

# OpenShift Migration Advisor — release notes — `v0.19.0`

Compare: `v0.18.0` → `v0.19.0`

## Appliance changes

### Features
- Added application and process details to VM views, including application counts in the VM table, per-VM application and process lists, filtering by application with certification status, and navigation between the Applications tab and filtered VM lists
- Bulk exclude and include now processes all selected VMs in a single operation, improving performance for large selections
- Improved data collection architecture by isolating each collection run into its own database with connection pooling and automatic cleanup of idle connections

### Fixes
- Improved VDDK version mismatch error message to clearly display the required vCenter and VDDK versions
- Fixed VM exclusion operations to complete atomically, preventing partially updated inventory data
- Replaced the Show excluded VMs toggle with a Report inclusion filter (Included/Excluded) that persists across tab switches
- Fixed credentials API returning HTTP 500 instead of 404 when credentials have been deleted
- Fixed group assessment report reverting to full vCenter data after excluding a VM from the group's Virtual Machines tab

## Console changes

### Features
- Added issues breakdown chart to the VM Migration Status card, showing VM counts by severity category with PDF export support
- Added VMware plan selection (VCF, VVF, VVS) and configurable discount percentages for VMware, Red Hat, and AAP solutions in the cost estimation form
- Added backfill capability to republish historical assessment data to the event stream, with an OpenShift Job template for one-time execution

### API changes (not yet available in the UI)
- Added Storage I/O Control (SIOC) information to the datastore inventory API, including enablement status, congestion threshold, and throughput settings

### Fixes
- Fixed compact mode sizing to correctly validate workload fit before applying node count constraints, and restored the compactMode field in stored cluster-requirements input
- Fixed inconsistent Last updated date formatting in the Assessments table and added a hover tooltip showing the exact timestamp
