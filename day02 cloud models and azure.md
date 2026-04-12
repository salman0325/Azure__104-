
# ☁️ 1. IaaS (Infrastructure as a Service)

### 📌 Definition:

👉 Cloud provider gives **hardware (VM, storage, network)**
👉 You manage everything else

---

### 💡 Real Example:

👉 Amazon Web Services EC2

* You create a VM
* Install OS
* Manage software yourself

---

### 💰 Cost:

👉 **Medium cost**

---

### ✅ Advantages:

* Full control
* Flexible
* Custom setup

### ❌ Disadvantages:

* Maintenance is your responsibility
* Security is also your responsibility

---

# 🧑‍💻 2. PaaS (Platform as a Service)

### 📌 Definition:

👉 Provider gives **platform (OS + runtime + tools)**
👉 You only deploy application

---

### 💡 Real Example:

👉 Microsoft Azure App Service

* Upload code
* Everything else is handled automatically

---

### 💰 Cost:

👉 **Medium to High**

---

### ✅ Advantages:

* No OS management
* Fast deployment
* Developer friendly

### ❌ Disadvantages:

* Less control
* Vendor lock-in risk

---

# 🌐 3. SaaS (Software as a Service)

### 📌 Definition:

👉 Use ready-made software
👉 No need to manage anything

---

### 💡 Real Example:

👉 Gmail
👉 Microsoft 365

---

### 💰 Cost:

👉 **Low to Medium (subscription based)**

---

### ✅ Advantages:

* No setup
* Easy to use
* No maintenance

### ❌ Disadvantages:

* No control
* Limited customization
* Internet dependency

---

# ⚖️ Comparison (Simple)

| Feature    | IaaS   | PaaS        | SaaS |
| ---------- | ------ | ----------- | ---- |
| Control    | High   | Medium      | Low  |
| Cost       | Medium | Medium-High | Low  |
| Management | More   | Medium      | None |

---

# 🌍 1. What is a Region?

### 📌 Definition:

👉 **Region = a geographic location** where cloud provider has **multiple data centers**

👉 Example:

* AWS → Mumbai Region
* Azure → UAE Region

---

### 🧠 Simple:

👉 Region = cloud location (city/country)

---

# 🏢 What is inside a Region?

👉 Multiple **Availability Zones (AZs)**

* Usually **2–6 AZs**

---

# 📏 Distance Between Regions

👉 Can be **hundreds to thousands of km**

👉 Example:

* Mumbai → Frankfurt

---

### ❓ Why far apart?

* Disaster safety
* High availability

---

# 🔗 2. What is Middleware?

### 📌 Definition:

👉 **Middleware = software between application and OS**

---

### 💡 Examples:

* Apache
* Nginx
* Tomcat

---

### 🧠 Simple:

👉 Middleware = connection layer

---

# 📜 3. What is Compliance?

### 📌 Definition:

👉 Following **rules and laws for security and privacy**

---

### 💡 Examples:

* Data protection laws
* Security standards

---

### 🧠 Simple:

👉 Compliance = follow rules

---

# ☁️ Services in a Region

👉 Depends on provider

* AWS → 200+ services total
* Per region → **50–150+ services**

---

# 🖥️ Deployment Types

## 1. Single Datacenter + Single VM

👉 One server, one VM

📌 Problem:
❌ If datacenter fails → everything down

---

## 2. Single Datacenter + Multiple VMs

👉 Multiple VMs in one datacenter

📌 Advantage:
✔ Load distribution

📌 Problem:
❌ Datacenter failure → all down

---

## 3. Multiple Datacenters

👉 VMs in different locations

📌 Advantage:
✔ Disaster recovery

---

## 🌎 4. Multiple Regions

👉 Use multiple regions

📌 Use case:
✔ Global apps
✔ Better performance

---

# 🏢 5. Availability Zone (AZ)

👉 AZ = **separate data centers inside a region**

📌 Important:

* Physically separate
* Independent power & network

---

# 📏 6. Range (Distance / Latency)

👉 Same AZ → very fast ⚡
👉 Different AZ → slightly slower
👉 Different Region → more delay

---

# 🔁 Real Example

👉 Region: Mumbai
👉 AZs: 3

* AZ-1 → Web VM
* AZ-2 → Database VM
* AZ-3 → Backup

👉 Second Region → Disaster backup

---

# 🧠 Easy Formula

👉 **VM → Datacenter → AZ → Region**

---

# ☁️ Management of Azure Infrastructure

## 🔹 Account

👉 Account = login to Azure
👉 Example: **portal.azure.com**

---

## 🔹 Resource

👉 Resource = any service you create

💡 Example:

* VM
* Database
* Storage

---

## 🔹 Resource Group

👉 Resource Group = **collection (folder) of resources**

💡 Example:
👉 One Resource Group contains:

* VM
* Database
* Storage

📌 Important:
👉 Same related resources are kept in one group

---

### ❓ Why use Resource Group?

* Easy management
* Organize resources
* Apply permissions
* Easy delete (delete all resources together)

---

## 🔹 Subscription

### 📌 Definition:

👉 Subscription = **billing unit in Azure**

👉 All resources are linked to a subscription

---

### 💡 Types of Subscription:

* Free subscription
* Pay-as-you-go
* Enterprise subscription

---

## 🏗️ Hierarchical Structure

👉 Azure structure:

**Account → Subscription → Resource Group → Resource**

---

## 💰 Billing Account (Simple)

👉 Billing is managed at **subscription level**

👉 To check billing:

* Go to Azure Portal
* Open Subscription
* Check **Billing section**

---

