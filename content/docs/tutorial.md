---
title: "Tutorial"
linkTitle: "Tutorial"
weight: 2
---

# How to Use Migration Assessment

This tutorial covers two methods to assess your VMware environment for migration to OpenShift Virtualization.

**Choose your assessment method:**

- **[RVTools Flow](#rvtools-flow)** - Upload an existing RVTools Excel export for instant assessment
- **[Discovery Agent Flow](#discovery-agent-flow)** - Deploy an OVA to vCenter for live discovery

---

## RVTools Flow

Upload an existing RVTools export file for instant assessment. Watch the video tutorial below:

<iframe width="700px" height="400px" src="https://interact.redhat.com/share/pkPLJELVr45LbdXg3InF" title="OpenShift Migration Advisor Using RVtools Flow" frameborder="0" referrerpolicy="unsafe-url" allowfullscreen="true" style="border-radius: 10px"></iframe>

### Prerequisites: RVTools File Requirements

Before uploading your RVTools export, ensure your Excel file meets the following requirements. The migration assessment tool validates your RVTools export and will report errors or warnings based on what's present.

#### Hard Requirements (Errors)

If these are missing, the upload will **fail**. All of these reside in the **vInfo** sheet:

| Requirement | Why? |
|-------------|------|
| **vInfo** sheet must have at least 1 row | No VMs means there is no inventory to plan |
| Column **VM ID** must not be null/empty | Used as the primary unique identifier for VMs |
| Column **VM** (Name) must not be null/empty | Used to identify and display the VM |
| Column **CLUSTER** must not be null/empty | Used to group VMs by clusters |

#### Soft Requirements (Warnings)

The following sheets are checked, but if they are empty or missing, the tool will only issue a **warning**. The inventory will still be built, but specific data points will be blank:

| Sheet | Impact if Missing |
|-------|-------------------|
| **vHost** | Host-related info will be unavailable |
| **vDatastore** | Storage/datastore info will be missing |
| **vNetwork** | Network configuration details will be missing |
| **vCPU** | Detailed CPU metrics (like core counts) will be missing |
| **vMemory** | RAM allocation details will be missing |
| **vDisk** | Disk size and provisioning data will be missing |
| **vNic** | Network interface details (IPs/MACs) will be missing |

Export your RVTools data with **all sheets enabled** to ensure the most comprehensive migration assessment. 

[Watch the Demo](https://interact.redhat.com/share/pkPLJELVr45LbdXg3InF)
---

## Discovery Agent Flow

Deploy a discovery agent to your vCenter for live environment analysis. Watch the video tutorial below:

<iframe width="700px" height="400px" src="https://interact.redhat.com/share/kEinYphM8Zyt7wXLys53?mode=videoOnly" title="Configure OpenShift Migration Advisor Agent Flow in Red Hat" frameborder="0" referrerpolicy="unsafe-url" allowfullscreen="true" allow="clipboard-write" sandbox="allow-popups allow-popups-to-escape-sandbox allow-scripts allow-forms allow-same-origin allow-presentation" style="border-radius: 10px"></iframe>

[Watch the Demo](https://interact.redhat.com/share/kEinYphM8Zyt7wXLys53)

