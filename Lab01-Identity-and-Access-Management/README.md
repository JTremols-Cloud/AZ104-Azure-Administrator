# Lab 01 – Identity and Access Management

This lab marks the beginning of Tremols Tech’s Azure Cloud Foundation project. As an early‑stage MSP contracted by ClearView Dental Associates, a mid‑size dental organization with multiple clinics and 180 employees, Tremols Tech is responsible for modernizing their IT operations by migrating identity, governance, and core workloads into Microsoft Azure.

Before compute, networking, storage, or clinical applications can be deployed, Tremols Tech must establish a secure identity and governance baseline. This lab implements the core identity, RBAC, subscription organization, and policy enforcement controls required for a production‑ready landing zone. Every workload ClearView Dental Associates migrates — VMs, storage, networking, analytics — will inherit the identity and governance controls established in this phase.

###### This is Phase 1 of a hands-on scenario modeled on an MSP cloud adoption engagement.

## 📘 Lab Overview

ClearView Dental Associates is preparing to migrate practice management systems, imaging workloads, and clinic operations into Azure. Tremols Tech must first establish: 

- Clean and compliant identity structure
- Role‑based access control aligned with least privilege
- Management group hierarchy for subscription governance
- Azure Policy enforcement for tagging, compliance, and resource hygiene
- Resource protection to prevent accidental deletion

###### This lab walks through the exact steps MSPs take when onboarding healthcare organizations into Azure, especially those with HIPAA sensitive workloads. 



## 🔐 Part 1 - Identity: Users, Guests \& Groups

This section focuses on core identity objects in Microsoft Entra ID.

### Scenario

Tremols Tech is onboarding its internal cloud engineers and external dental software vendors into Azure so they can support ClearView Dental Associates during the migration.

### Tasks Completed

#### 1. Created Internal User Accounts

I added a new internal user representing a ClearView Regional Manager and configured identity metadata:

- Display name
- Job title
- Department
- Usage location

###### This account represents the first wave of ClearView identities being migrated into Azure.

#### 2. Invited an External Guest User

Invited an external imaging software consultant to simulate a B2B scenario. The guest appeared in Entra ID and received an email invitation.

#### 3. Created the "Tremols Tech - Engineering" Security Group

I created a security group to centralize access for the Engineering department.

- Assigned myself as owner
- Added internal and external users
- Reviewed static vs dynamic membership

###### Dynamic membership requires P1/P2 licensing and is extremely useful for MSP environments. For this lab, assigned membership was used.



## 🏛 Part 2 - Governance: Management Groups & RBAC

This section covers subscription organization and role‑based access control (RBAC).

### Scenario

ClearView Dental Associates wants consistent access control and governance across all Azure subscriptions. Tremols Tech must implement a management group hierarchy and apply RBAC at the correct scope to support future clinical workloads, imaging systems, and patient data applications.

### Tasks Completed

#### 1. Created a Management Group

I created a management group (clearview-mg-core) named "ClearView Dental - Core Governance" to organize subscriptions under a centralized governance boundary for all current and future Azure workloads.

Management groups enable:
- Centralized RBAC
- Centralized Azure Policy
- Subscription inheritance
- Directory‑level governance

#### 2. Assigned a Built-in Role

I assigned the Virtual Machine Contributor role to the Tremols Tech Engineering group at the management group scope.

This role allows VM management without OS access or network/storage configuration, which is ideal for engineering and support teams working with dental clinics.

#### 3. Created a Custom RBAC Role

I cloned the Support Request Contributor role and removed unnecessary permissions to enforce least privilege.

Custom role included:
- Actions for support ticket creation
- NotActions to block provider registration
- Assignable scope limited to the management group

#### 4. Monitored Role Assignments

I used the Activity Log to confirm role creation and assignment events, which is essential for MSP auditing and compliance.



## 🛡 Part 3 - Governance Enforcement: Azure Policy, Tagging & Locks

This section enforces governance using Azure Policy, tagging, and resource locks.

### Scenario

During an internal audit, Tremols Tech discovered resources missing ownership, project, and cost center metadata. For a dental organization with strict compliance requirements, consistent tagging is essential for cost visibility, automation, and HIPAA aligned governance.

### Tasks Completed

#### 1. Applied Tags to a Resource Group

I created a new resource group (clearview-rg-governance) and applied a CostCenter: 000 tag.

Tags help with:
- Cost management
- Ownership tracking
- Automation
- Reporting

#### 2. Enforced Tagging with Azure Policy

I assigned a built‑in policy requiring the CostCenter tag on all resources in the resource group.
Attempting to create a storage account without the tag resulted in a policy violation, which confirms enforcement.

#### 3. Applied Tag Inheritance via Azure Policy

I replaced the enforcement policy with a Modify policy that automatically applies the CostCenter tag to child resources.

This required:
- A remediation task
- A managed identity

###### Creating a new storage account showed the tag automatically applied.

#### 4. Configured Resource Locks
- Applied a Delete lock to the governance resource group.
- Attempting to delete the group resulted in a lock violation, confirming protection.
- Locks apply regardless of role, so even Owners must remove the lock first.



## 📝 Notes & Observations

- Management groups are essential for MSP‑style subscription organization.
- RBAC roles should always be assigned to groups, not individuals.
- Custom roles help enforce least privilege.
- RBAC controls who can act, Policy controls what can be deployed, and locks prevent accidental changes or deletion.
- Tagging is critical for cost management, automation, and operational clarity.
- Remediation tasks bring existing resources into compliance.
- Locks apply regardless of role, so even Owners must remove the lock before deleting.
- Identity and governance mistakes compound over time, establishing a clean baseline in Phase 1 prevents costly rework in later phases.



## 🎯 Why This Lab Matters

Identity and governance are the backbone of Azure.

This lab establishes Tremols Tech’s operational foundation for ClearView Dental Associates:
- Who can access what
- How subscriptions are organized
- How resources are governed
- How metadata is enforced
- How accidental deletion is prevented

###### Everything else (compute, networking, storage, analytics) depends on this layer being clean, secure, and well structured.


## 🧹 Cleanup

To remove lab resources:
Portal

* Delete the resource group
* Delete the management group
* Remove policy assignments

### PowerShell
```powershell
Remove-AzResourceGroup -Name rg-clearview-governance
Remove-AzManagementGroup -GroupName mg-clearview-core
```

### CLI
```bash
az group delete --name rg-clearview-governance
az account management-group delete --name mg-clearview-core
```

###### This completes Phase 1 of Tremols Tech’s MSP cloud adoption project.



## 📈 Next Lab

➡️ Lab 02 - Compute & Virtual Machines

