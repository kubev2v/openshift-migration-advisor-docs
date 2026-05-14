---
title: "Cost Estimation For Partners"
linkTitle: "Cost Estimation For Partners"
description: "Calculate cost estimation for VMware to OpenShift Virtualization migrations"
weight: 5
---

# Cost Estimation For Partners

The Cost Estimation feature provides cost analysis for migrating VMware environments to OpenShift Virtualization. It compares three-year cost projections across VMware VCF, VMware VVF, and OpenShift Virtualization scenarios to help partners guide migration decisions.

{{% alert title="Partner-Only Feature" color="info" %}}
Cost estimation is available exclusively to Red Hat partners. Partner authentication is required to access this functionality.
{{% /alert %}}

Applies to: V0.11.0
Last update (dd-mm-yyyy): 12-05-2026

---

## How It Works

The cost estimation service analyzes your VMware cluster inventory to calculate three-year cost projections. It extracts environment data from your assessment and applies proprietary cost models to generate comparative cost breakdowns.

### High-Level Flow

```
1. Partner authenticates to the API
2. Select an assessment and cluster for cost analysis
3. Optional: Apply discount percentages for each vendor
4. Service extracts customer environment data from cluster inventory:
   - Total ESXi hosts
   - CPU sockets per host
   - CPU cores per socket
   - Total virtual machines
5. External cost estimation service calculates costs for three scenarios:
   - VMware VCF (VMware Cloud Foundation)
   - VMware VVF (VMware vSphere Foundation)
   - OpenShift Virtualization
6. Response includes cost breakdowns and savings analysis
```

---

## Prerequisites

### Partner Access

- Valid Red Hat partner credentials
- Partner authentication token
- Read permission on the target assessment

### Assessment Requirements

- Assessment must have at least one snapshot
- Snapshot must contain inventory data
- Cluster must exist in the inventory with the specified cluster ID

---

## API Workflow

### Step 1: Authenticate as Partner

Ensure you have valid partner credentials and authentication token. The cost estimation endpoint validates partner status before processing requests.

### Step 2: Calculate Cost Estimation

Request a cost estimation calculation for a specific cluster within an assessment.

```bash
curl -X POST http://planner:3443/api/v1/assessments/{assessment-id}/cost-estimation \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <partner-token>" \
  -d '{
    "clusterId": "cluster-1",
    "discounts": {
      "vcfDiscountPct": 0,
      "vvfDiscountPct": 0,
      "redhatDiscountPct": 0,
      "aapDiscountPct": 0
    }
  }'
```

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `clusterId` | Yes | - | ID of the VMware cluster from the assessment inventory |
| `discounts.vcfDiscountPct` | No | 0 | VMware VCF discount percentage (0-100) |
| `discounts.vvfDiscountPct` | No | 0 | VMware VVF discount percentage (0-100) |
| `discounts.redhatDiscountPct` | No | 0 | Red Hat discount percentage (0-100) |
| `discounts.aapDiscountPct` | No | 0 | Ansible Automation Platform discount percentage (0-100) |

### Response Codes

| Code | Meaning |
|------|---------|
| **200** | Cost estimation calculation successful |
| **400** | Bad request (missing clusterId, invalid discounts) |
| **401** | Unauthorized (invalid or missing authentication) |
| **403** | Forbidden (requires partner access) |
| **404** | Assessment or cluster not found |
| **500** | Internal error |
| **503** | Cost estimation service unavailable |

---

## Understanding Results

### Response Structure

The cost estimation response includes:

```json
{
  "calculatorVersion": "1.0.0",
  "results": {
    "vmwareVcf": { ... },
    "vmwareVvf": { ... },
    "openshiftVirtualization": { ... }
  },
  "savings": {
    "vsVcf": { ... },
    "vsVvf": { ... }
  }
}
```

### Calculator Version

The `calculatorVersion` field indicates which version of the cost calculation model was used. This allows tracking of estimate methodology over time.

### Cost Scenarios

Each scenario provides:

| Field | Description |
|-------|-------------|
| `totalThreeYearCostEstimation` | Total projected cost in USD over 3 years |
| `breakdown` | Detailed cost components (see below) |

### Cost Breakdown Components

Each scenario breaks down costs into six categories:

| Component | Description |
|-----------|-------------|
| `softwareSubscriptions` | Core platform subscription costs |
| `ansibleAutomationPlatform` | AAP licensing and subscription |
| `migrationConsultingServices` | Professional services for migration |
| `swingHardwareUpgrades` | Temporary hardware for migration swing |
| `additionalStorageCosts` | Storage infrastructure costs |
| `thirdPartyIsvCosts` | Third-party vendor software costs |

{{% alert title="Note" color="warning" %}}
The specific algorithms and multipliers used to calculate these cost components are proprietary and confidential. Cost estimates are based on Red Hat's internal pricing models and industry analysis.
{{% /alert %}}

### Savings Analysis

When OpenShift Virtualization is more cost-effective than VMware options, the `savings` field provides:

| Savings Field | Description |
|---------------|-------------|
| `vsVcf.absoluteThreeYearUsd` | Total USD saved over 3 years vs VMware VCF |
| `vsVcf.percentage` | Savings as percentage of VMware VCF cost |
| `vsVvf.absoluteThreeYearUsd` | Total USD saved over 3 years vs VMware VVF |
| `vsVvf.percentage` | Savings as percentage of VMware VVF cost |

---

## Customer Environment Data Extraction

The service automatically extracts the following data from your cluster inventory to inform cost calculations:

| Data Point | Source | Notes |
|------------|--------|-------|
| Total ESXi Hosts | Cluster infrastructure inventory | Total host count from inventory |
| Sockets per Host | First host CPU configuration from inventory | Extracted from `cpuSockets` field; defaults to 2 if unavailable |
| Cores per Socket | Calculated from first host CPU data | Calculated as `cpuCores / cpuSockets`; defaults to 16 if unavailable or invalid |
| Total Virtual Machines | Cluster VM count from inventory | Total VM count across the cluster |

The service attempts to extract actual CPU configuration from the first host in your inventory. If CPU data is missing or invalid, it falls back to industry-standard defaults (2 sockets per host, 16 cores per socket).

---

## Cost Estimation Methodology

The cost estimation feature uses a proprietary calculation model developed by Red Hat to project three-year costs. The methodology considers:

- Customer environment sizing (hosts, sockets, cores, VMs)
- Vendor subscription models and pricing tiers
- Migration consulting service requirements
- Infrastructure upgrade needs for migration
- Third-party software dependencies
- Discount percentages applied by the user

{{% alert title="Classified Information" color="warning" %}}
Specific pricing formulas, cost multipliers, and algorithmic details are classified and cannot be disclosed in public documentation. Cost estimates are based on Red Hat's confidential pricing intelligence and market analysis.
{{% /alert %}}

---

## Error Handling

### Common Errors

| Error | Cause | Resolution |
|-------|-------|------------|
| **403 Forbidden** | Non-partner user attempting access | Verify partner credentials and authentication |
| **404 Not Found** | Assessment or cluster doesn't exist | Verify assessment ID and cluster ID from inventory |
| **400 Bad Request - clusterId required** | Missing clusterId in request | Include clusterId in request body |
| **400 Bad Request - no snapshots** | Assessment has no inventory data | Create an assessment with valid inventory |
| **400 Bad Request - empty inventory** | Latest snapshot has no inventory | Re-run inventory collection |
| **503 Service Unavailable** | Cost estimation service is down | Contact system administrator |

---

## Tips

- **Use Latest Inventory**: Cost calculations are based on the latest snapshot. Ensure your assessment inventory is up-to-date before requesting estimates.
- **Accurate Discount Data**: Apply accurate discount percentages to get realistic cost comparisons. Consult with vendor account teams for current discount rates.
- **Multiple Clusters**: Generate separate cost estimates for each cluster if your environment has multiple VMware clusters with different configurations.
- **Partner Context**: Cost estimates are designed for partner-led customer conversations. Use results as discussion points, not final pricing.
- **Version Tracking**: Note the `calculatorVersion` in your results. Estimates from different calculator versions may not be directly comparable.

