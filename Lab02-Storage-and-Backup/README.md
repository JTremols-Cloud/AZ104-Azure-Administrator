# Lab 02: Storage & Backup 🚧 In progress

> Part of the [AZ-104 Azure Administrator Journey](../README.md). ClearView Dental Associates and all names, accounts, and data are fictional. No real patient data was used. This lab is based on Microsoft's AZ-104 learning content and is not affiliated with Microsoft.

**Exam domain:** Implement and manage storage; Monitor and maintain Azure resources | **Outcome:** Secure, cost-aware storage and a tested backup and disaster recovery baseline for ClearView's data.

## Contents

1. [Business Scenario](#business-scenario)
2. [Cost & Safety Notes](#cost--safety-notes)
3. [Walkthrough](#walkthrough)
4. [Results, Challenges & What I Learned](#results-challenges--what-i-learned)
5. [Production Considerations](#production-considerations)
6. [Cleanup](#cleanup)

---

## Business Scenario

ClearView Dental Associates keeps imaging archives and patient documents on aging on-premises file servers. Most files are rarely opened after the first few weeks. Tremols Tech needs to move that data into Azure so that:

- rarely used files cost less to store
- access is private, authenticated, and time-limited
- files can't be deleted or altered during a retention period
- VM-based practice systems can be backed up and recovered after accidental or malicious data loss
- a regional outage doesn't take down critical systems

This lab builds on the [Lab 01](../01-identity-and-governance/) baseline: resources follow the same naming convention and carry the `CostCenter: 000` tag.

**What this lab covers**

- Storage accounts and redundancy (RA-GRS)
- Lifecycle management
- Blob containers, immutable storage, and SAS tokens
- Azure Files and Storage Browser
- Network restriction with service endpoints
- Recovery Services vaults and Azure Backup
- Azure Site Recovery (VM replication)

**Prerequisites**

| Requirement | Details |
|---|---|
| Azure subscription | Pay-As-You-Go |
| Azure role | Owner on the subscription |
| Tools | Azure Portal, with CLI equivalents for reference |
| Lab files | VM template and parameters from Microsoft's AZ-104 learn path |

# 🚧 In-progress and actively working on it
