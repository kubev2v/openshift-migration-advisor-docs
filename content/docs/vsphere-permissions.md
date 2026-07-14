---
title: "vSphere Permissions"
linkTitle: "vSphere Permissions"
description: "Minimum vSphere privileges required for each Discovery Agent operation mode"
weight: 3
---

# Minimum vSphere Permissions

The Discovery Agent validates vSphere privileges before attempting each operation. If a required privilege is missing, the agent reports the operation as unavailable rather than failing mid-run.

You can create one custom vSphere role per operation mode, or a single combined role that enables all three. Grant each role at the **datacenter** level and propagate to child objects unless noted otherwise.

---

## Inventory Collection (Read-Only)

The minimum privileges for basic inventory scanning:

| Privilege | Purpose |
|-----------|---------|
| `System.Read` | Read inventory objects (VMs, hosts, datastores, networks) |
| `System.View` | View objects in the vSphere inventory tree |

Assign on the datacenter and propagate to all four root folders (VM, Host, Datastore, Network).

---

## Deep Inspection (Snapshot-Based Disk Analysis)

Adds snapshot privileges on top of the collection privileges:

| Privilege | Purpose |
|-----------|---------|
| `System.Read` | Required for inventory access |
| `System.View` | Required for inventory access |
| `VirtualMachine.State.CreateSnapshot` | Create a temporary snapshot of the VM for disk analysis |
| `VirtualMachine.State.RemoveSnapshot` | Remove the snapshot after analysis completes |

The collection privileges (`System.Read`, `System.View`) must be granted at the datacenter level. The snapshot privileges can be scoped to the **VM folder only**.

---

## OVA Deployment & Forecaster Benchmarks

The full privilege set for deploying the agent OVA and running storage benchmarks:

| Privilege | Purpose |
|-----------|---------|
| `System.Read` | Required for inventory access |
| `System.View` | Required for inventory access |
| `Datastore.AllocateSpace` | Allocate storage for deployed VM disks |
| `Datastore.Browse` | Browse datastore contents during deployment |
| `Datastore.DeleteFile` | Clean up temporary files after deployment |
| `Datastore.FileManagement` | Manage files on the datastore during OVA import |
| `VirtualMachine.Inventory.Create` | Register the deployed VM in the inventory |
| `VirtualMachine.Inventory.Delete` | Remove the benchmark VM after completion |
| `VirtualMachine.Provisioning.Clone` | Clone or deploy the OVA template |
| `VirtualMachine.Interact.PowerOn` | Power on the deployed VM |
| `VirtualMachine.Config.AddRemoveDevice` | Configure virtual hardware on the deployed VM |

Assign at the datacenter level and propagate to all four root folders (VM, Host, Datastore, Network).

For details on the forecaster's temporary resources and benchmarking workflow, see [Migration Forecaster](../forecaster/).

---

## Choosing a Role

If you need only inventory collection, the two `System.*` privileges are sufficient. Add the snapshot privileges for deep disk inspection, and the full set when you deploy the agent as an OVA with forecaster benchmarks.

The agent's credential verification endpoint checks these privileges at runtime and reports any missing ones before operations begin.
