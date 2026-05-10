# Active Directory (AD) vs Entra ID (Azure AD)

## 1. What is Active Directory (ADDS)?

Active Directory

Active Directory Domain Services (ADDS) is Microsoft ka **on-premises identity system**.

Ye mostly office/company ke local servers par install hota hai.

### ADDS kya karta hai?

* User management
* Computer management
* Login authentication
* Group Policy
* Centralized control

### Example

Company me:

* 500 users
* 300 PCs
* Sabko ek hi username/password se login

ADDS ye sab manage karta hai.

---

# 2. What is Entra ID (Azure AD)?

Microsoft Entra ID

Pehle iska naam Azure AD tha.

Ye Microsoft ka **cloud-based identity provider** hai.

### Entra ID use hota hai:

* Microsoft 365
* Azure
* SaaS Apps
* Cloud login
* MFA
* SSO

---

# Main Difference

| Feature         | ADDS                 | Entra ID            |
| --------------- | -------------------- | ------------------- |
| Location        | On-premises          | Cloud               |
| Protocol        | LDAP, Kerberos, NTLM | OAuth, SAML, OpenID |
| Device Join     | Domain Join          | Azure/Entra Join    |
| Internet Needed | No                   | Yes                 |
| Group Policy    | Yes                  | Limited             |
| Best For        | Internal office      | Cloud apps          |

---

# Authentication vs Authorization

## Authentication = “Who are you?”

User prove karta hai:

* username
* password
* MFA

Example:

```text
Username: salman
Password: Salman123
```

System bolta:
✅ Yes you are Salman

---

## Authorization = “What can you access?”

Login ke baad:

* kya open kar sakta hai?
* kya delete kar sakta hai?
* admin hai ya read-only?

Example:

* Reader → sirf dekh sakta
* Contributor → create/update
* Owner → full control

---

# Azure Licenses

## Free License

Basic features:

* Users/groups
* Basic authentication

---

## P1 License

Advanced features:

* Conditional Access
* Dynamic Groups
* Self-service password reset

---

## P2 License

Security advanced:

* Identity Protection
* Privileged Identity Management (PIM)
* Risk-based MFA

---

# Identity Objects in Entra ID

## 1. User

Human account.

Example:

```text
salman@company.com
```

---

## 2. Group

Users ka collection.

Example:

```text
DevOps-Team
HR-Team
```

Benefits:

* One time permission assignment
* Easier management

---

## 3. Service Principal

Application identity.

Example:

* Terraform
* Jenkins
* GitHub Actions

Agar app Azure resources access kare → Service Principal use hota hai.

---

# Cloud Identities vs ADDS

| Identity Type   | Meaning                      |
| --------------- | ---------------------------- |
| Cloud Identity  | Directly Entra ID me created |
| Synced Identity | ADDS se sync hua             |
| Guest Identity  | External user                |

---

# Guest Account

External user.

Example:

```text
abc@gmail.com
```

Aap usko tenant me invite karte ho.

Use Case:

* Vendor
* Client
* Freelancer

---

# Directory Synchronized Users

ADDS user sync hokar cloud me aata hai.

Tool:

```text
Azure AD Connect
```

Example:

```text
On-prem AD → Entra ID
```

---

# MFA (Multi Factor Authentication)

2-step verification.

Example:

1. Password
2. OTP/mobile approval

Benefits:

* Password leak hone par bhi protection

---

# Bulk Operations

Ek saath multiple users create/update/delete.

CSV file use hoti hai.

Example CSV:

```csv
Name,UPN,Password
Ali,ali@company.com,Pass123
Ahmed,ahmed@company.com,Pass123
```

---

# RBAC (Role Based Access Control)

Azure permissions system.

## RBAC decide karta hai:

“Kaun kya kar sakta hai Azure resources par?”

---

# Azure Hierarchy

```text
Management Group
   ↓
Subscription
   ↓
Resource Group
   ↓
Resource
```

---

# 1. Management Group

Multiple subscriptions manage.

Big companies use karti hain.

---

# 2. Subscription

Billing boundary.

Example:

* Production Subscription
* Dev Subscription

---

# 3. Resource Group

Resources ka container.

Example:

```text
RG-Production
```

---

# 4. Resource

Actual service:

* VM
* Storage
* VNET

---

# Built-in Roles

## 1. Owner

Full access + permissions manage.

Can:

* Create
* Delete
* Assign roles

---

## 2. Contributor

Everything except role assignment.

Can:

* Create VM
* Delete storage

Cannot:

* Give permissions

---

## 3. Reader

Sirf view.

Cannot modify.

---

## 4. User Access Administrator

Permissions manage kar sakta hai.

Can:

* Assign RBAC roles

Cannot:

* Manage resources fully

---

# Custom Role

Apni permission create karna.

Example:

```text
Can restart VM
Cannot delete VM
```

---

# Role Assignment Components

RBAC me 3 cheezein hoti hain:

| Component          | Meaning       |
| ------------------ | ------------- |
| Security Principal | User/Group/SP |
| Role Definition    | What allowed  |
| Scope              | Where applied |

---

# Scope Example

```text
Contributor
   assigned to
DevOps-Team
   on
Resource Group
```

---

# Entra ID Roles vs Azure RBAC Roles

| Entra ID Roles    | Azure RBAC Roles          |
| ----------------- | ------------------------- |
| Identity manage   | Azure resources manage    |
| User/group manage | VM/storage/network manage |
| Tenant level      | Resource level            |

---

# Examples

## Entra Role

```text
Global Administrator
User Administrator
```

Works on:

* Users
* MFA
* Identity

---

## Azure RBAC Role

```text
Owner
Contributor
Reader
```

Works on:

* Azure resources

---

# Most Dangerous RBAC Mistakes

## 1. Too Many Owners

Problem:

* Everyone full admin

Fix:

* Least privilege

---

## 2. Direct User Assignments

Problem:

* Hard to manage

Fix:

* Use groups

---

## 3. Assigning Roles at Subscription Level

Problem:

* Huge access exposure

Fix:

* Use Resource Group scope

---

## 4. Not Using MFA

Problem:

* Account compromise

Fix:

* Enable MFA

---

## 5. Old Unused Accounts

Problem:

* Security risk

Fix:

* Regular audit

---

# Password Reset Methods

## Method 1 — Admin Reset

Admin portal se reset.

---

## Method 2 — Self Service Password Reset (SSPR)

User khud reset karta hai:

* OTP
* Email
* Phone

---

# COMPLETE REAL SCENARIO

# Company Scenario

Company:

```text
ABC Pvt Ltd
```

Need:

* 2 admins
* 10 developers
* 5 HR users

Resources:

* VM
* Storage
* Database

---

# Design

## Entra ID

Create:

* Users
* Groups
* MFA

Groups:

```text
Dev-Team
HR-Team
Admins
```

---

# RBAC

| Group    | Role        | Scope        |
| -------- | ----------- | ------------ |
| Admins   | Owner       | Subscription |
| Dev-Team | Contributor | Dev-RG       |
| HR-Team  | Reader      | HR-RG        |

---

# LAB (STEP BY STEP)

# LAB 1 — Create User

## Step 1

Open:

[Microsoft Azure Portal](https://portal.azure.com?utm_source=chatgpt.com)

---

## Step 2

Search:

```text
Microsoft Entra ID
```

---

## Step 3

Left side:

```text
Users
```

---

## Step 4

Click:

```text
+ New User
```

---

## Step 5

Fill:

```text
User name: salman
Name: Salman Khan
Password: Auto generate
```

Click:

```text
Create
```

---

# LAB 2 — Create Group

## Step 1

Go:

```text
Groups
```

---

## Step 2

Click:

```text
New Group
```

---

## Step 3

Fill:

```text
Group Type: Security
Name: DevOps-Team
```

---

## Step 4

Add members.

Click:

```text
Create
```

---

# LAB 3 — Enable MFA

## Step 1

Go:

```text
Protection
→ Conditional Access
```

---

## Step 2

Click:

```text
New Policy
```

---

## Step 3

Select:

```text
Users → All Users
```

---

## Step 4

Grant:

```text
Require MFA
```

Enable policy.

---

# LAB 4 — Assign RBAC Role

## Step 1

Open:

```text
Resource Group
```

---

## Step 2

Click:

```text
Access Control (IAM)
```

---

## Step 3

Click:

```text
Add Role Assignment
```

---

## Step 4

Choose:

```text
Contributor
```

---

## Step 5

Select:

```text
DevOps-Team
```

---

## Step 6

Click:

```text
Review + Assign
```

---

# LAB 5 — Reset Password

## Method 1

```text
Users
→ Select User
→ Reset Password
```

---

## Method 2

Enable:

```text
Password Reset
```

Then user resets from:

```text
https://passwordreset.microsoftonline.com
```

---

# REAL INTERVIEW SHORT ANSWER

## What is ADDS?

On-premises identity management system.

---

## What is Entra ID?

Cloud identity and access management system.

---

## Authentication?

Identity verification.

---

## Authorization?

Permission control.

---

## Difference between RBAC and Entra Roles?

RBAC:

* Azure resources permissions

Entra Roles:

* Identity management permissions

---

# SHORT VISUAL

```text
User Login
   ↓
Authentication
   ↓
Entra ID verifies password + MFA
   ↓
Authorization
   ↓
RBAC checks permissions
   ↓
Access Granted
```
