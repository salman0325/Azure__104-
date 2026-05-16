# Azure Storage

## What is Microsoft Azure Storage?

Azure Storage is a cloud service used to store data on Azure.
It can store:

* Files
* Images
* Videos
* Backups
* Logs
* Messages
* Big data

It is:

* Highly available
* Secure
* Scalable
* Durable

---

# Azure Storage Account

## What is Storage Account?

A **Storage Account** is the main container/resource in Azure that holds storage services.

Inside one storage account you can create:

* Blob Storage
* File Shares
* Queue
* Table

Think:

```text
Storage Account
 ├── Blob
 ├── File Share
 ├── Queue
 └── Table
```

---

# Features of Storage Account

## 1. Scalability

Can store TBs/PBs of data.

## 2. High Availability

Data copies are created automatically.

## 3. Security

Supports:

* Encryption
* RBAC
* SAS Token
* Private Endpoint

## 4. Different Access Tiers

Hot / Cool / Archive.

## 5. Multiple Access Methods

Can access using:

* Portal
* CLI
* SDK
* REST API

---

# Types of Azure Storage

---

# 1. Blob Storage

Used to store:

* Images
* Videos
* Backup files
* Logs
* ISO files

Example:

```text
Netflix videos
Website images
VM backup
```

---

# Blob Types

## A. Block Blob

Most common.

Used for:

* Images
* Videos
* Documents

Best for streaming/uploading.

Example:

```text
.mp4
.jpg
.pdf
```

---

## B. Append Blob

Data is appended only at end.

Used for:

* Logging
* Audit files

Example:

```text
Application logs
Server logs
```

---

## C. Page Blob

Stores data in pages.

Used for:

* Virtual machine disks (VHD)

Example:

```text
Azure VM disk
```

---

# 2. Azure Files

Managed file sharing service.

Uses SMB/NFS protocol.

Looks like shared network drive.

Example:

```text
Shared office files
Lift-and-shift apps
```

---

# 3. Queue Storage

Stores messages.

Used for communication between applications.

Example:

```text
Order placed → queue → processing server
```

Useful in:

* Microservices
* Background jobs

---

# 4. Table Storage

NoSQL key-value storage.

Stores structured data.

Example:

```text
User profile
IoT device data
```

Cheap and fast.

---

# Redundancy in Azure Storage

Redundancy = extra copies of data.

Purpose:

```text
Protect data from failure/disaster.
```

---

# 1. LRS — Locally Redundant Storage

## Copies:

3 copies

## Location:

Same datacenter.

## Use:

Cheap option.

## Best for:

Non-critical data.

Example:

```text
Dev/Test environment
```

Diagram:

```text
Datacenter
 ├─ Copy1
 ├─ Copy2
 └─ Copy3
```

---

# 2. ZRS — Zone Redundant Storage

## Copies:

3 copies

## Location:

Different Availability Zones.

## Use:

Protect from datacenter failure.

## Best for:

Production apps.

Diagram:

```text
Zone1 → Copy1
Zone2 → Copy2
Zone3 → Copy3
```

---

# 3. GRS — Geo Redundant Storage

## Copies:

6 copies

## Location:

3 local + 3 secondary region.

## Use:

Disaster recovery.

## Best for:

Business critical apps.

Diagram:

```text
Primary Region
 ├─ 3 copies

Secondary Region
 ├─ 3 copies
```

---

# 4. GZRS — Geo Zone Redundant Storage

## Copies:

6 copies

## Location:

Zones + secondary region.

## Best redundancy.

## Use:

Mission critical applications.

Diagram:

```text
Primary Region Zones
 ├─ Zone1
 ├─ Zone2
 └─ Zone3

Secondary Region
 └─ 3 copies
```

---

# Which Redundancy Should Use?

| Type | Copies | Best Use           |
| ---- | ------ | ------------------ |
| LRS  | 3      | Cheap/testing      |
| ZRS  | 3      | High availability  |
| GRS  | 6      | Disaster recovery  |
| GZRS | 6      | Maximum protection |

---

# Hierarchical Namespace (HNS)

HNS is used in:

## Azure Data Lake Storage Gen2

It creates:

```text
Folder + directory structure
```

Like Linux filesystem.

---

# Without HNS

Blob storage behaves flat.

Example:

```text
container/file1
container/file2
```

Folders are fake.

No real directory.

---

# With HNS

Real folders/directories exist.

Example:

```text
container/
   sales/
      2026/
         jan.csv
```

---

# Why HNS Useful?

Useful for:

* Big data
* Analytics
* Hadoop/Spark

Benefits:

* Faster operations
* Better permissions
* Real directory management

---

# Version-Level Immutability Support

Immutability means:

```text
Data cannot be changed/deleted.
```

Version-level immutability locks blob versions.

Used for:

* Compliance
* Legal records
* Backup protection
* Ransomware protection

Example:

```text
Financial documents
Audit records
```

---

# Blob Access Tiers

---

# 1. Hot Tier

Frequently accessed data.

## Cost:

* High storage cost
* Low access cost

## Use:

Daily used files.

Example:

```text
Website images
```

---

# 2. Cool Tier

Less frequently accessed.

## Cost:

* Lower storage cost
* Higher access cost

## Use:

Monthly backups.

---

# 3. Archive Tier

Rarely accessed.

## Cost:

Very cheap storage.

## Access:

Slow retrieval.

## Use:

Long-term backup.

Example:

```text
7-year old records
```

---

# Security Features

## Encryption

Data encrypted automatically.

## SAS Token

Temporary secure access link.

## RBAC

Role-based access.

## Firewall

Restrict IP access.

## Private Endpoint

Private network access.

---

# Important Azure Storage Concepts

---

# Lifecycle Management

Automatically move data:

```text
Hot → Cool → Archive
```

Saves cost.

---

# Soft Delete

Deleted files can recover.

Like recycle bin.

---

# Snapshot

Read-only copy of blob.

Used for:

* Backup
* Recovery

---

# Static Website Hosting

Blob storage can host static websites.

Example:

```text
HTML/CSS/JS website
```

---

# CDN Integration

Faster content delivery globally.

---

# Mount Azure Files

Can mount like:

```text
Z: drive
```

on Windows/Linux.

---

# Data Lake Storage Gen2

Blob storage + HNS.

Used for:

* Big data
* Analytics
* AI/ML

---

# Storage Account Types

| Type               | Use            |
| ------------------ | -------------- |
| General Purpose v2 | Most common    |
| Blob Storage       | Blob optimized |
| FileStorage        | Premium files  |
| BlockBlobStorage   | Premium blob   |

---



# Real Interview Questions

## Difference between Blob and File Storage?

| Blob           | File              |
| -------------- | ----------------- |
| Object storage | Shared filesystem |
| HTTP access    | SMB/NFS           |
| Images/videos  | Shared folders    |

---

## Difference between Queue and Table?

| Queue               | Table           |
| ------------------- | --------------- |
| Messages            | Structured data |
| Async communication | NoSQL storage   |

---

# Easy Real Example

## YouTube Example

| Service    | Use              |
| ---------- | ---------------- |
| Blob       | Videos           |
| Queue      | Video processing |
| Table      | Metadata         |
| File Share | Shared files     |
