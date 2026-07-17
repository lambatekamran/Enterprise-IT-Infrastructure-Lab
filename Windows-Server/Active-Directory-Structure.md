# Phase 3 – Active Directory Organizational Structure & User Management

## Enterprise IT Infrastructure Lab

## Project Overview

This phase focuses on designing and implementing the Active Directory structure for the fictional company **TechNova Solutions**. A well-planned Active Directory environment improves administration, security, scalability, and resource management.

---

# Objectives

The objectives of this phase are to:

* Design an enterprise Organizational Unit (OU) structure
* Create department-based Security Groups
* Create employee user accounts
* Assign users to the correct departments
* Implement role-based access management
* Document the Active Directory design

---

# Company Information

| Item             | Value               |
| ---------------- | ------------------- |
| Company          | TechNova Solutions  |
| Domain           | technova.local      |
| Server           | TECH-DC01           |
| Active Directory | Windows Server 2022 |

---

# Organizational Unit Design

The Organizational Units (OUs) are designed to logically organize users, computers, and administrative objects.

## OU Structure

```text
technova.local
│
├── Management
├── Human Resources
├── Finance
├── Information Technology
├── Sales
├── Computers
├── Servers
├── Groups
└── Service Accounts
```

## Purpose of Each OU

| OU                     | Purpose                                    |
| ---------------------- | ------------------------------------------ |
| Management             | Executive and management user accounts     |
| Human Resources        | HR department users                        |
| Finance                | Finance department users                   |
| Information Technology | IT staff accounts                          |
| Sales                  | Sales department users                     |
| Computers              | Domain-joined client computers             |
| Servers                | Member servers                             |
| Groups                 | Security and distribution groups           |
| Service Accounts       | Accounts used by applications and services |

---

# Naming Convention

## Organizational Units

Department names are used for clarity and consistency.

Example:

```text
Finance
Information Technology
Sales
```

---

# Security Groups

Security Groups are used to assign permissions based on department or job role.

## Group Configuration

| Group Name    | Scope  | Type     |
| ------------- | ------ | -------- |
| IT_Admins     | Global | Security |
| HR_Users      | Global | Security |
| Finance_Users | Global | Security |
| Sales_Users   | Global | Security |
| Managers      | Global | Security |

---

# User Accounts

The following sample users were created.

| Full Name     | Username | Department             | Security Group |
| ------------- | -------- | ---------------------- | -------------- |
| John Smith    | jsmith   | Management             | Managers       |
| Sarah Ahmed   | sahmed   | Human Resources        | HR_Users       |
| David Lee     | dlee     | Finance                | Finance_Users  |
| Michael Brown | mbrown   | Information Technology | IT_Admins      |
| Emma Wilson   | ewilson  | Sales                  | Sales_Users    |

Each user account was configured with:

* User must change password at next logon
* Standard user permissions
* Department-specific group membership

---

# Group Membership Strategy

Role-Based Access Control (RBAC) was implemented using Security Groups.

Example:

```text
Michael Brown
        │
        ▼
IT_Admins
        │
        ▼
Administrative permissions

Sarah Ahmed
        │
        ▼
HR_Users
        │
        ▼
HR shared resources
```

This design simplifies permission management and follows the principle of least privilege.

---

# PowerShell Automation

Organizational Units can be created automatically using PowerShell.

Example:

```powershell
Import-Module ActiveDirectory

$OUs = @(
"Management",
"Human Resources",
"Finance",
"Information Technology",
"Sales",
"Computers",
"Servers",
"Groups",
"Service Accounts"
)

foreach ($OU in $OUs) {
    New-ADOrganizationalUnit -Name $OU -Path "DC=technova,DC=local"
}
```

Automation reduces manual effort and ensures consistent deployments.

---

# Verification

The following checks were completed:

* Verified all Organizational Units were created successfully.
* Verified Security Groups exist.
* Verified user accounts were created.
* Verified users are located in the correct OU.
* Verified users are members of the appropriate Security Groups.

---

# Screenshots

The following screenshots document this phase:

1. Active Directory Users and Computers console
2. Organizational Unit structure
3. Security Groups
4. User account creation wizard
5. User properties and group membership
6. Completed Active Directory structure

All screenshots are stored in:

```text
/Screenshoots/Active Directory
```

---

# Skills Demonstrated

This phase demonstrates the following skills:

* Active Directory Administration
* Organizational Unit Design
* Identity and Access Management (IAM)
* User Account Management
* Security Group Administration
* Role-Based Access Control (RBAC)
* Windows Server Administration
* PowerShell Automation
* Enterprise Documentation

---

# Lessons Learned

During this phase, a structured Active Directory environment was created to support centralized administration and future expansion. Department-based Organizational Units and Security Groups provide a scalable foundation for implementing Group Policy, file permissions, and delegated administration.

---

# Next Phase

The next phase of the project is **DNS Server Configuration**, where the following tasks will be completed:

* Configure Forward Lookup Zones
* Configure Reverse Lookup Zones
* Create Host (A) Records
* Configure Alias (CNAME) Records
* Configure Pointer (PTR) Records
* Verify DNS name resolution using `nslookup`
* Document the DNS infrastructure for GitHub
