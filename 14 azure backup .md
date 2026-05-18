# Azure Backup — Complete Guide

## What is Microsoft Azure Backup?

Microsoft Azure Backup is a cloud-based backup service in Microsoft Azure used to:

* Protect data
* Recover deleted files
* Restore servers/VMs after failure
* Protect against ransomware

It stores backups inside:

* **Recovery Services Vault (RSV)**

---

# Why Azure Backup is Used

## Real World Uses

* VM crash recovery
* Accidental file deletion
* Ransomware recovery
* Database restore
* Disaster recovery

Example:

```text id="7c1qth"
Company VM deleted accidentally
→ Restore from backup
```

---

# Azure Backup Architecture

![Image](https://images.openai.com/static-rsc-4/PYg0jQUFmH33_Jn9wSwtKfVpyryC-pWwnSD1z4O1vy-KASDCFnLF41vgL_NsDV0cN55XO_MnJspH9MF7kKzzvAG5mxhhLtSwo1qHuAGhUDgPV-Wr0VrpqrP41gkrFnLhIp0TaXv60ozatmPyfUlfePQLqW5dRKmQHuC0eUdzXKDkXzBM2d-ewAu9Ak1PCHW_?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/gJAy1xoMZDDXiGUyPlf_GMiOdnCqkjWF6QU7u5n3tY_CNmjmGPp3z1ieVdHp1fS8Ovewi7pPG7v0AhhbdQI561nJbtPg2eq6Ym-ATO4o13IzIHoWm0XfiAenT1wPAJKQZYiiuVqNtvjJevW1f22RQhdVMHvHeu_XWqiLJvSvL8rEwmDBfdfKcCDP22BF2Blz?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/pjefgp5ASpcMqDPxUwkCxkOmSxKICcAgFVLDiFTwZk53Mp24OrL_siPGk6_otTQQduY1NG4EhyoVkEfmMAwbUXBCpnoadvVPo74nMk79nuBlusCmWvS9RTCa98REdFTcJtZpLxzaJUF9kl7AZ-ZBEWD4kjNDmMxGlRJsQtj7JPuXiAH4GY2Ih-eKkVIOx1dm?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/KZ_3TnZXXm3ybZgmEvqo79RnkjdfZVtcTV2Zaqpofm6DC6nsGJcRdyDj0h397NCzqay_7M44sCI-E5DnhLQku9Rq6E0d9VCLfvLfyunVslvGLrBSq_Kfsgf1TL1M8_ALJmf35sLUOmEYmSGFKR7tZLw0u7YQPhOK0LEbEC5R7V9ZTZBWwzhoVye0lFNgnAKu?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/NPIjKII-i477FqVHJY8bDgtSFct4Z1EWjgCB9Bz4_XUKOBEK21tT6s7uCd9n5c7xf1uZ-88jJV4FX7K0J-tVD-zRck-KsGuM5uu0Lj_zZnliRN7MwDNgd9wf2C8XFcYGYJTBlFxvmOnJbYDjh_R4MTt7nled26VMYoD3O-fNp8_Krc2tiiQdFgUdpJEjgeRX?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/-Bx2x8y_HSEEzYk_OU7ZkE5UpLqdEf7DCaz0lEIgHwkMXlx-DtK0LlqAO_9b_M1gcbigRRKuDVirU0Elsq10_Zog1SnLBqLURihcKxeVCDMDM3wK-QOd1bsQ6zsaZOFMJIz9Q6VCRU2PYddY6DUNZ7iL2m7MNM63111MTpsEKXSKLp9QJ5Iz5QRakWD1mxxQ?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/nh01TSN1tQ4jmIMIwGduWgbjEVn4EUqS3SlquW1qOmYm0aL9we7pdWx8D-Mcg9DzG6wDR0jPImDUUq9j3_D51lQSCh_Bu3QMe2bSi8Nt-IdB33mF-DzTDJqbyph6FirK7j4vVcDgsEKySrtIQPbIqBZ2KbcLdbRUhaVtE2U--6WF3X9J4Ox6EUN3KBNWBs31?purpose=fullsize)

Flow:

```text id="8qog8z"
Azure VM
   ↓
Backup Policy
   ↓
Recovery Services Vault
   ↓
Backup Storage
```

---

# Main Components

| Component               | Purpose                    |
| ----------------------- | -------------------------- |
| Recovery Services Vault | Stores backup data         |
| Backup Policy           | Defines schedule/retention |
| Backup Agent            | Sends data to Azure        |
| Snapshot                | Point-in-time copy         |
| Restore Point           | Recovery version           |

---

# Recovery Services Vault (RSV)

## What is RSV?

Special storage container used for:

* Backup
* Restore
* Disaster recovery

One vault can protect:

* Azure VMs
* Files
* SQL databases
* On-premises servers

---

# Backup Types in Azure

## 1. Azure VM Backup

Used for:

* Virtual machines

Features:

* App-consistent backup
* Automatic snapshots
* Point-in-time restore

---

## 2. Azure Files Backup

Protects:

* File shares

---

## 3. SQL Backup in Azure VM

Protects:

* SQL Server databases inside VMs

---

## 4. SAP HANA Backup

Protects:

* SAP workloads

---

## 5. On-Premises Backup

Uses:

* MARS Agent
* Azure Backup Server

---

# Backup Concepts

## 1. Backup Policy

Defines:

* Backup timing
* Retention period

Example:

```text id="1lm8k4"
Daily backup at 10 PM
Keep backup for 30 days
```

---

## 2. Retention Policy

Controls:

* How long backups stay

Types:

* Daily
* Weekly
* Monthly
* Yearly

---

## 3. Restore Point

Specific backup copy used for recovery.

---

## 4. Snapshot

Temporary quick copy before vault storage.

---

# Backup Storage Redundancy

## 1. LRS (Locally Redundant Storage)

* 3 copies
* Same region
* Cheapest

```text id="6m4ot9"
Datacenter failure protection limited
```

---

## 2. GRS (Geo-Redundant Storage)

* Secondary region copy
* Better disaster recovery

```text id="d09l4h"
Primary region fails
→ backup available in another region
```

---

# Azure Backup Security Features

## Soft Delete

Deleted backups remain recoverable for 14 days.

---

## Multi-User Authorization (MUA)

Extra approval required for critical operations.

---

## Encryption

Backup data encrypted:

* In transit
* At rest

---

## Immutable Vault

Prevents backup deletion/modification.

Useful against ransomware.

---

# Azure Backup Pricing Factors

Depends on:

* Number of protected instances
* Backup storage size
* Redundancy type

---

# Important Azure Backup Terms

| Term               | Meaning                  |
| ------------------ | ------------------------ |
| Vault              | Backup storage container |
| Backup Policy      | Schedule settings        |
| Restore Point      | Recovery copy            |
| Snapshot           | Temporary image          |
| Retention          | Backup duration          |
| Protected Instance | Backed-up resource       |

---

# LAB 1 — Backup Azure VM

## Real World Scenario

```text id="lz1tbm"
Company wants daily backup of production VM.
```

---

# Step-by-Step Lab

## Step 1 — Create Recovery Services Vault

Go to:

```text id="wb06zx"
portal.azure.com
```

Search:

```text id="68pt58"
Recovery Services Vaults
```

Click:

```text id="dbi7ms"
Create
```

Fill:

| Setting        | Value             |
| -------------- | ----------------- |
| Subscription   | Your subscription |
| Resource Group | backup-rg         |
| Vault Name     | prod-backup-vault |
| Region         | Same as VM        |

Click:

```text id="gk1s4c"
Review + Create
→ Create
```

---

## Step 2 — Open Vault

Click:

```text id="7sgz2x"
Go to Resource
```

---

## Step 3 — Configure Backup

Inside vault:

```text id="a65d7j"
Backup
```

Choose:

| Field                       | Value           |
| --------------------------- | --------------- |
| Where is workload running?  | Azure           |
| What do you want to backup? | Virtual Machine |

Click:

```text id="s6zhm1"
Backup
```

---

## Step 4 — Select VM

Click:

```text id="l42m0z"
Select Virtual Machines
```

Choose VM:

```text id="jlwm7z"
prod-vm01
```

Click:

```text id="3oy3bg"
OK
```

---

## Step 5 — Create Backup Policy

Default policy:

```text id="okd0kr"
Daily backup
30-day retention
```

Or click:

```text id="j3z4uo"
Create New
```

Custom example:

* Daily at 11 PM
* Retain 90 days

---

## Step 6 — Enable Backup

Click:

```text id="m6f8fd"
Enable Backup
```

Backup starts.

---

## Step 7 — Run Manual Backup

Inside VM backup page:

```text id="vl3n7q"
Backup Now
```

Choose retention:

```text id="r6h6iw"
30 days
```

Click:

```text id="7a3mgw"
OK
```

---

# Restore VM

## Step 1

Open:

```text id="wk3m3n"
Recovery Services Vault
```

---

## Step 2

Go:

```text id="q2nxz9"
Backup Items
→ Azure Virtual Machine
```

---

## Step 3

Select VM:

```text id="5af02o"
prod-vm01
```

---

## Step 4

Click:

```text id="4a09q7"
Restore VM
```

Choose restore point.

---

## Step 5

Restore options:

* Create new VM
* Replace existing VM

Click:

```text id="l6zqpn"
Restore
```

---

# LAB 2 — Azure File Share Backup

## Real World Scenario

```text id="mbu6iy"
Company file server deleted accidentally.
Need fast restore.
```

---

# Step 1 — Create Storage Account

Search:

```text id="j6brsm"
Storage Accounts
```

Click:

```text id="21qvdn"
Create
```

---

# Step 2 — Create File Share

Go:

```text id="4a9t1o"
Data Storage
→ File Shares
```

Click:

```text id="zwvkkq"
+ File Share
```

Name:

```text id="i9jsl9"
companyfiles
```

---

# Step 3 — Enable Backup

Open:

```text id="3qspux"
companyfiles
```

Click:

```text id="9lmzz1"
Backup
```

Choose:

```text id="o5ivv9"
Recovery Services Vault
```

Create/select vault.

---

# Step 4 — Configure Policy

Example:

* Daily backup
* 60-day retention

Click:

```text id="b7l72n"
Enable Backup
```

---

# Restore Files

Go:

```text id="ex5j5h"
Recovery Services Vault
→ Backup Items
→ Azure Storage
```

Select:

```text id="5xt3n3"
Restore Share
```

Choose:

* Entire share
* Individual file

Restore complete.

---

# LAB 3 — SQL Server Backup in Azure VM

## Real World Scenario

```text id="ng4xgk"
Company database corrupted after update.
Need database recovery.
```

---

# Step 1 — Open Recovery Services Vault

Go:

```text id="ec0v0y"
Backup
```

Choose:

| Field       | Value                  |
| ----------- | ---------------------- |
| Workload    | Azure                  |
| Backup Type | SQL Server in Azure VM |

---

# Step 2 — Discover SQL VMs

Click:

```text id="2s92m0"
Start Discovery
```

Azure scans SQL VMs.

---

# Step 3 — Select Database

Choose:

```text id="7om5m5"
companydb
```

---

# Step 4 — Configure Backup

Policy example:

* Full backup weekly
* Differential daily
* Log backup every 15 minutes

---

# Step 5 — Enable Backup

Click:

```text id="0r7n9m"
Enable Backup
```

---

# Restore SQL Database

Go:

```text id="mrxv1g"
Backup Items
→ SQL in Azure VM
```

Select DB.

Click:

```text id="91p9dy"
Restore
```

Restore options:

* Original location
* Alternate database

---

# Important Exam Questions

## Short Questions

1. What is Azure Backup?
2. What is Recovery Services Vault?
3. Difference between LRS and GRS?
4. What is retention policy?
5. What is restore point?
6. What is soft delete?

---

# Interview Questions

## Q1. Difference between Backup and Site Recovery?

| Backup                | Site Recovery       |
| --------------------- | ------------------- |
| Data protection       | Disaster recovery   |
| Restore files/VMs     | Full failover       |
| Point-in-time restore | Business continuity |

---

## Q2. Why use immutable vault?

Answer:

```text id="iwy4vv"
Prevents attackers/ransomware from deleting backups.
```

---

# Best Practices

| Best Practice           | Reason                      |
| ----------------------- | --------------------------- |
| Use GRS                 | Better DR                   |
| Enable soft delete      | Protect accidental deletion |
| Use backup alerts       | Monitoring                  |
| Test restores regularly | Ensure backups work         |
| Use separate vaults     | Better management           |

---

# Complete Azure Backup Flow

```text id="yvyj5j"
Azure Resource
      ↓
Backup Policy
      ↓
Snapshot Created
      ↓
Recovery Services Vault
      ↓
Retention Applied
      ↓
Restore When Needed
```
