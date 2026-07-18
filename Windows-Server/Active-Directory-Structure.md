# Phase 3 – Active Directory Organizational Structure & User Management

## Enterprise IT Infrastructure Lab

## What is the Goal of This Phase?

In this phase, we built the **Active Directory structure** for our fictional company **TechNova Solutions**.

The goal is to organize the company's users, computers, and security groups in a way that is easy to manage as the company grows.

By the end of this phase, we have:

* Created Organizational Units (OUs)
* Created Security Groups
* Created employee user accounts
* Assigned users to the correct groups
* Prepared the environment for Group Policy and File Server permissions

---

# Why Do We Need Active Directory?

In a company with many employees, managing each computer separately is inefficient.

Active Directory allows an administrator to:

* Manage all users from one place
* Control who can access company resources
* Apply company policies
* Organize employees by department
* Improve security

Instead of configuring every computer individually, everything can be managed centrally.

---

# Lab Information

| Item             | Value               |
| ---------------- | ------------------- |
| Company          | TechNova Solutions  |
| Domain           | technova.local      |
| Server           | TECH-DC01           |
| Operating System | Windows Server 2022 |

---

# Step 1 – Create Organizational Units (OUs)

## What is an OU?

An **Organizational Unit (OU)** is like a folder inside Active Directory.

It helps organize users, computers, and groups by department.

For example:

* HR employees are stored in the HR OU.
* Finance employees are stored in the Finance OU.
* IT staff are stored in the Information Technology OU.

This makes administration much easier.

---

## OUs Created

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

### Screenshot 1

(<../Screenshoots/Active Directory/ou-structure.png>)

---

# Step 2 – Create Security Groups

## What is a Security Group?

A Security Group is used to give permissions to multiple users at the same time.

Instead of giving permissions to every employee individually, we add users to a group.

Example:

```text
Finance Folder

↓

Finance_Users Group

↓

David Lee
Sarah Ahmed
John Smith
```

Anyone added to **Finance_Users** automatically receives the correct permissions.

---

## Security Groups Created

| Group Name    | Scope  | Type     | Purpose            |
| ------------- | ------ | -------- | ------------------ |
| IT_Admins     | Global | Security | IT administrators  |
| HR_Users      | Global | Security | HR department      |
| Finance_Users | Global | Security | Finance department |
| Sales_Users   | Global | Security | Sales department   |
| Managers      | Global | Security | Management team    |

**Group Scope:** Global

**Group Type:** Security

### Screenshot 2

**Insert Screenshot:**

(<../Screenshoots/Active Directory/Groups-OU.png>)
---

# Step 3 – Create Employee Accounts

We created sample employee accounts for each department.

These accounts simulate a real company environment.

| Employee      | Username | Department             | Group         |
| ------------- | -------- | ---------------------- | ------------- |
| John Smith    | jsmith   | Management             | Managers      |
| Sarah Ahmed   | sahmed   | Human Resources        | HR_Users      |
| David Lee     | dlee     | Finance                | Finance_Users |
| Michael Brown | mbrown   | Information Technology | IT_Admins     |
| Emma Wilson   | ewilson  | Sales                  | Sales_Users   |

Each user was configured with:

* User must change password at next logon
* Standard user permissions
* Department-specific group membership

### Screenshot 3

(<../Screenshoots/Active Directory/users-created.png>)

---

# Step 4 – Add Users to Security Groups

Each employee was added to the appropriate Security Group.

Example:

```text
Michael Brown
        │
        ▼
IT_Admins
```

This allows permissions to be managed through groups instead of individual users.

### Screenshot 4

**Insert Screenshot:**

(<../Screenshoots/Active Directory/group-membership.png>)

---

# Why Is This Design Important?

This structure follows common enterprise practices.

Benefits include:

* Easy administration
* Better organization
* Improved security
* Easier troubleshooting
* Scalable as the company grows

For example, when a new Finance employee joins the company:

1. Create the user.
2. Place the user in the Finance OU.
3. Add the user to the **Finance_Users** group.

No other configuration is required.

---

# PowerShell Automation

Instead of creating each OU manually, we can automate the process.

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

Automation saves time and reduces mistakes.

---

# What We Learned

In this phase we learned how to:

* Design an Active Directory structure
* Organize departments using Organizational Units
* Create Security Groups
* Create employee accounts
* Assign users to groups
* Use PowerShell to automate administration

These are core tasks performed by Windows System Administrators in enterprise environments.

---

# Skills Demonstrated

* Windows Server Administration
* Active Directory
* Organizational Unit (OU) Management
* User Account Management
* Security Group Management
* Identity and Access Management (IAM)
* PowerShell Automation
* Enterprise Documentation

---

# Conclusion

The Active Directory environment is now organized and ready for the next stages of the project. In the following phases, these OUs and Security Groups will be used to apply **Group Policies**, configure **File Server permissions**, and manage access to company resources.

---

# Next Phase

**Phase 4 – DNS Server Configuration**

In the next phase, we will:

* Configure DNS
* Create Forward Lookup Zones
* Create Reverse Lookup Zones
* Create A, CNAME, and PTR records
* Test name resolution using `nslookup`
* Document the DNS infrastructure
