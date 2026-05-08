# 🔹 1. Availability Zone (AZ)

**Definition:**
Availability Zones are **physically separate datacenters** inside one region (like 3 different buildings with power, cooling, network isolation).

### ✔ Example

Region: East US
Zones: Zone1, Zone2, Zone3

---

## ✅ Use Case

* High availability (if one datacenter fails → app still runs)
* Disaster protection

---

## ✅ When to use AZ

* Production apps
* Critical workloads (banking, e-commerce)
* When you need **99.99% uptime**

---

## ❌ When NOT to use

* Small testing VM
* Budget constraints (cross-zone traffic cost)
* Simple dev environment

---

# 🔹 2. SLA (Service Level Agreement)

**Definition:**
Microsoft ka promise = uptime guarantee

### ✔ Example

* Single VM → ~99.9%
* VM in AZ → ~99.99%

👉 If SLA break hota → Azure gives **credits (refund)**

---

# 🔹 3. Custom Script Extension

**Definition:**
VM create hote waqt ya baad me **automatic script run karna**

### ✔ Use case

* Install Nginx
* Setup app automatically
* No manual SSH needed

---

# 🔹 4. VMSS (Virtual Machine Scale Set)

**Definition:**
Auto scaling group of VMs

### ✔ Work

* Increase VM → high load
* Decrease VM → low load

👉 Automatic scaling based on:

* CPU %
* Memory
* Requests

---

# 🔹 5. Azure Load Balancer (LB)

**Definition:**
Traffic ko multiple VMs me distribute karta hai

---

## 🔹 Types of Load Balancer

### 1. **Public Load Balancer**

* Internet traffic
* Example: website

### 2. **Internal Load Balancer**

* Private network traffic
* Example: backend servers

---

## 🔹 When to use which

| Situation        | Use         |
| ---------------- | ----------- |
| Internet website | Public LB   |
| Backend DB/app   | Internal LB |

---

## ✔ Advantages

* High availability
* Fault tolerance
* Load distribution

## ❌ Disadvantages

* Extra cost
* Config complexity

---

# 🔹 6. Generalize (Sysprep)

**Definition:**
VM ko template banane ke liye clean karna

### ✔ What it does

* Remove hostname
* Remove user data
* Remove SSH keys

👉 After this → VM image ban sakti hai

---

# 🔹 7. Resource Provider Registration

**Definition:**
Azure services enable karna

### ✔ Example

* VM → Microsoft.Compute
* Storage → Microsoft.Storage

👉 Without register → resource create nahi hoga

---
# 🔥 Azure VMSS + Load Balancer + Auto Scaling LAB (100% Step by Step)

Ye lab tumhe:

* VM create
* Nginx auto install
* Custom image
* VM Scale Set
* Load Balancer
* Auto scaling
* High Availability

sab practical sikha dega.

---

# 🧪 PHASE 1 — Create Ubuntu VM

## 🔹 Step 1: Open Azure

Go to:

[Microsoft Azure Portal](https://portal.azure.com?utm_source=chatgpt.com)

Login karo.

---

# 🔹 Step 2: Create VM

LEFT SIDE:

👉 Virtual Machines

Click:

👉 + Create
👉 Azure Virtual Machine

---

# 🔹 Step 3: Basics Tab

Fill EXACTLY:

| Option         | Value               |
| -------------- | ------------------- |
| Subscription   | Your subscription   |
| Resource Group | Create new          |
| Name           | vm-nginx            |
| Region         | Any                 |
| Image          | Ubuntu Server 22.04 |
| Size           | B1s                 |

---

# 🔹 Step 4: Administrator Account

| Option              | Value          |
| ------------------- | -------------- |
| Authentication Type | SSH Public Key |
| Username            | azureuser      |

Click:

👉 Generate new key pair

Popup ayega:

👉 Download private key

SAVE `.pem` file.

---

# 🔹 Step 5: Networking

| Option               | Value                |
| -------------------- | -------------------- |
| Public IP            | Enable               |
| Public inbound ports | Allow selected ports |
| Select inbound ports | SSH (22), HTTP (80)  |

---

# 🔹 Step 6: Advanced Tab (IMPORTANT)

Top tabs may click:

👉 Advanced

Scroll down:

👉 Custom data / cloud-init

Paste FULL script:

```bash
#!/bin/bash
apt update -y
apt install nginx -y
systemctl enable nginx
systemctl start nginx
echo "Hello From Azure VM" > /var/www/html/index.html
```

---

# 🔹 Step 7: Create VM

Click:

👉 Review + Create
👉 Create

Wait 2–5 min.

---

# 🧪 PHASE 2 — Test Nginx

## 🔹 Step 8: Copy Public IP

Go to:

👉 VM Overview

Copy:

👉 Public IP Address

Example:

```bash
20.xx.xx.xx
```

---

# 🔹 Step 9: Open Browser

Open:

```bash
http://PUBLIC-IP
```

You should see:

```bash
Hello From Azure VM
```

Means:

* VM working
* Nginx working
* Automation working

---

# 🧪 PHASE 3 — Create Custom Image

## 🔹 Step 10: Stop VM

Go to VM.

Click:

👉 Stop

Wait until:

```bash
Stopped (deallocated)
```

---

# 🔹 Step 11: Capture Image

Inside VM:

👉 Capture

Fill:

| Option                  | Value       |
| ----------------------- | ----------- |
| Image Name              | nginx-image |
| Automatically delete VM | No          |

IMPORTANT:

✔ Check:

```bash
Generalized
```

Click:

👉 Create

Wait few minutes.

---

# 🧪 PHASE 4 — Create VM Scale Set (VMSS)

## 🔹 Step 12: Create VMSS

Search:

👉 Virtual Machine Scale Sets

Click:

👉 + Create

---

# 🔹 Step 13: Basics

Fill:

| Option         | Value      |
| -------------- | ---------- |
| Resource Group | Same       |
| VMSS Name      | nginx-vmss |
| Region         | Same       |
| Orchestration  | Uniform    |

---

# 🔹 Step 14: Image Selection

Click:

👉 My Items

Select:

👉 nginx-image

---

# 🔹 Step 15: Size

Choose:

```bash
B1s
```

---

# 🔹 Step 16: Authentication

| Option   | Value        |
| -------- | ------------ |
| Username | azureuser    |
| SSH Key  | Use existing |

Upload your `.pem` public key.

---

# 🔹 Step 17: Instance Count

Set:

```bash
2
```

Means:

* 2 VMs create hongi automatically

---

# 🧪 PHASE 5 — Load Balancer Setup

## 🔹 Step 18: Load Balancer

Networking tab may:

Select:

| Option         | Value               |
| -------------- | ------------------- |
| Load Balancing | Azure Load Balancer |
| Type           | Public              |

Azure automatically:

* LB create karega
* Backend pool
* Health probe

sab khud.

---

# 🧪 PHASE 6 — Auto Scaling

## 🔹 Step 19: Enable Autoscaling

Scaling tab may:

Select:

```bash
Enable Autoscaling
```

---

# 🔹 Step 20: Configure Scale Rules

## RULE 1 — Increase VM

Click:

👉 Add Rule

Set:

| Option    | Value             |
| --------- | ----------------- |
| Metric    | Percentage CPU    |
| Operator  | Greater than      |
| Threshold | 70                |
| Operation | Increase count by |
| Count     | 1                 |

---

## RULE 2 — Decrease VM

Add another rule:

| Option    | Value             |
| --------- | ----------------- |
| Metric    | Percentage CPU    |
| Operator  | Less than         |
| Threshold | 30                |
| Operation | Decrease count by |
| Count     | 1                 |

---

# 🔹 Step 21: Create VMSS

Click:

👉 Review + Create
👉 Create

Wait 5–10 min.

---

# 🧪 PHASE 7 — Test Load Balancer

## 🔹 Step 22: Get Load Balancer IP

Go:

👉 VMSS
👉 Overview

Copy:

👉 Public IP

Open browser:

```bash
http://PUBLIC-IP
```

Nginx page ayega.

---

# 🔹 Step 23: Connect VM Instances

Go:

👉 VMSS
👉 Instances

You will see:

```bash
instance 0
instance 1
```

---

# 🔹 Step 24: SSH into Instance 1

Connect using:

```bash
ssh -i key.pem azureuser@PUBLIC-IP
```

Change page:

```bash
echo "SERVER 1" | sudo tee /var/www/html/index.html
```

---

# 🔹 Step 25: SSH into Instance 2

Do same:

```bash
echo "SERVER 2" | sudo tee /var/www/html/index.html
```

---

# 🔹 Step 26: Refresh Browser

Open LB IP again:

```bash
http://LOAD-BALANCER-IP
```

Refresh multiple times.

You will see:

* SERVER 1
* SERVER 2

alternating.

Means:
✅ Load balancing working.

---

# 🧪 PHASE 8 — Test Auto Scaling

## 🔹 Step 27: Install Stress Tool

SSH into any VM.

Run:

```bash
sudo apt update
sudo apt install stress -y
```

---

# 🔹 Step 28: Generate CPU Load

Run:

```bash
stress --cpu 2
```

This increases CPU usage.

---

# 🔹 Step 29: Observe Scaling

Go Azure Portal:

👉 VMSS
👉 Instances

After few minutes:

New VM automatically create hogi.

Means:
✅ Auto scaling working.

---

# 🔥 FINAL ARCHITECTURE

```bash
Users
   ↓
Load Balancer
   ↓
VMSS
 ├── VM1 (Nginx)
 ├── VM2 (Nginx)
 └── VM3 (Auto Created)
```

---

# 🔥 High Availability Achieved

Tumne achieve kiya:

✅ Auto Healing
✅ Auto Scaling
✅ Load Balancing
✅ High Availability
✅ Custom Image
✅ Infrastructure Automation




---



# 🔥 Final Summary

* AZ = High availability
* SLA = uptime guarantee
* VMSS = auto scaling
* LB = traffic distribution
* Sysprep = image ready
* Custom Script = automation
* Resource Provider = service enable

---

