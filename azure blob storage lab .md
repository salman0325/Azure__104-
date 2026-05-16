# LAB 1 — Azure Blob Storage Using GUI (Azure Portal)

## Goal

Create:

* Storage Account
* Blob Container
* Upload File
* Access Blob

---

# Step 1 — Open Azure Portal

Go to:
[Microsoft Azure Portal](https://portal.azure.com?utm_source=chatgpt.com)

Login.

---

# Step 2 — Create Resource Group

Search:

```text id="0h1wkp"
Resource Groups
```

Click:

```text id="5jlwmc"
Create
```

Fill:

| Setting             | Value   |
| ------------------- | ------- |
| Resource Group Name | my-rg   |
| Region              | East US |

Click:

```text id="hn0r94"
Review + Create → Create
```

---

# Step 3 — Create Storage Account

Search:

```text id="oj42fu"
Storage Accounts
```

Click:

```text id="7y11si"
Create
```

Fill:

| Setting              | Value          |
| -------------------- | -------------- |
| Resource Group       | my-rg          |
| Storage Account Name | mystorage12345 |
| Region               | East US        |
| Performance          | Standard       |
| Redundancy           | LRS            |

Click:

```text id="k5q21h"
Review + Create → Create
```

Wait deployment complete.

---

# Step 4 — Open Storage Account

Click:

```text id="y6mxvd"
Go to resource
```

---

# Step 5 — Create Blob Container

Left menu:

```text id="es6yy7"
Data Storage → Containers
```

Click:

```text id="p7teqv"
+ Container
```

Fill:

| Setting       | Value   |
| ------------- | ------- |
| Name          | images  |
| Public Access | Private |

Click:

```text id="l4hzxq"
Create
```

---

# Step 6 — Upload File

Open:

```text id="5prq72"
images
```

Click:

```text id="o98jpw"
Upload
```

Select:

```text id="vteh1w"
test.txt or image
```

Click:

```text id="q19v5v"
Upload
```

---

# Step 7 — Access Blob URL

Click uploaded file.

Copy:

```text id="d87brm"
Blob URL
```

Example:

```text id="m7m1f5"
https://mystorage12345.blob.core.windows.net/images/test.txt
```

---

# What You Learned

✅ Storage Account creation
✅ Blob container creation
✅ File upload
✅ Blob access

---

# LAB 2 — Azure File Share Using GUI

## Goal

Create:

* Azure File Share
* Upload shared file

---

# Step 1 — Open Storage Account

Go:

```text id="8rv9ck"
Storage Account
```

---

# Step 2 — Create File Share

Left menu:

```text id="a0mvrv"
Data Storage → File Shares
```

Click:

```text id="8ny3r2"
+ File Share
```

Fill:

| Setting | Value                 |
| ------- | --------------------- |
| Name    | sharedfiles           |
| Tier    | Transaction Optimized |

Click:

```text id="8r4nqk"
Create
```

---

# Step 3 — Upload File

Open:

```text id="8g7w6t"
sharedfiles
```

Click:

```text id="r7q9qa"
Upload
```

Select file.

Click:

```text id="4pr7pv"
Upload
```

---

# Step 4 — Connect File Share to Windows VM/PC

Inside file share click:

```text id="y1z6rm"
Connect
```

Azure automatically gives PowerShell command.

Example:

```powershell id="ot3qgm"
net use Z: \\mystorage12345.file.core.windows.net\sharedfiles
```

Run command on Windows machine.

Now shared drive appears like:

```text id="5xh1pf"
Z: drive
```

---

# What You Learned

✅ File Share creation
✅ Shared storage
✅ SMB mounting
✅ Shared file access

---

# LAB 3 — Queue Storage Using GUI

## Goal

Create queue and add message.

---

# Step 1 — Open Storage Account

---

# Step 2 — Open Queues

Left menu:

```text id="vuxkl4"
Data Storage → Queues
```

Click:

```text id="s9ylsy"
+ Queue
```

Name:

```text id="cx8t9h"
appqueue
```

Click:

```text id="f4vf3k"
OK
```

---

# Step 3 — Add Message

Open queue.

Click:

```text id="0e7gpo"
Add Message
```

Enter:

```text id="67pk5o"
order-created
```

Click:

```text id="5o4o5t"
OK
```

---

# What Queue Used For?

Example:

```text id="ehm4jz"
Website order → Queue → Backend processing
```

---

# LAB 4 — Table Storage Using GUI

## Goal

Create NoSQL table.

---

# Step 1 — Open Storage Account

---

# Step 2 — Open Tables

Left menu:

```text id="n0ry7r"
Data Storage → Tables
```

Click:

```text id="jktmqt"
+ Table
```

Name:

```text id="0jqmgq"
employee
```

Click:

```text id="3xqkt8"
OK
```

---

# What Table Storage Used For?

Example:

```text id="g7g26q"
Employee data
IoT sensor data
User profiles
```

---

# Mini Practice Tasks

## Practice 1

Create:

```text id="3u4u88"
hot tier blob container
```

Upload:

```text id="l95rnp"
10 images
```

---

## Practice 2

Create:

```text id="gprpfr"
cool tier backup storage
```

---

## Practice 3

Enable:

```text id="40vfj8"
Soft Delete
Versioning
```

Then test recovery.

---

# Important GUI Areas in Storage Account

| Section              | Purpose                 |
| -------------------- | ----------------------- |
| Containers           | Blob storage            |
| File Shares          | Shared filesystem       |
| Queues               | Messaging               |
| Tables               | NoSQL                   |
| Networking           | Firewall/private access |
| Access Keys          | Authentication          |
| Lifecycle Management | Auto tier movement      |
| Data Protection      | Soft delete/versioning  |

---

# Real Architecture Example

## Video Streaming App

| Service      | Use                  |
| ------------ | -------------------- |
| Blob Storage | Videos               |
| Queue        | Video encoding jobs  |
| Table        | Metadata             |
| File Share   | Shared admin reports |
