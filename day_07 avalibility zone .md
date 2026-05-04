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

# 🔥🔥🔥 LAB (Step by Step – Scratch)

---

# 🧪 LAB 1

## 🔹 Step 1: Create VM

1. Azure Portal → Virtual Machines
2. Click **Create**
3. Select:

   * Image: Ubuntu
   * Size: B1s
4. Authentication:

   * SSH key
5. Networking:

   * Public IP → Enable
6. Click **Review + Create**

---

## 🔹 Step 2: Add Custom Script (Advanced)

During VM creation:

👉 Go to **Advanced tab**

Paste script:

```bash
#!/bin/bash
apt update
apt install -y nginx
systemctl start nginx
```

👉 This will auto install Nginx

---

## 🔹 Step 3: Test VM

* Copy Public IP
* Open browser
  👉 You should see **Nginx page**

---

## 🔹 Step 4: Create Custom Image

1. Go to VM
2. Click **Stop**
3. Click **Capture**
4. Check:

   * ✔ Generalized
5. Create Image

---

## 🔹 Step 5: Create VMSS

1. Go to VM Scale Set
2. Click **Create**
3. Select:

   * Image = your custom image
4. Set:

   * Instance count = 2
5. Enable:

   * Autoscaling

---

## 🔹 Step 6: Configure Auto Scaling

1. Go to VMSS → Scaling
2. Add rule:

👉 If CPU > 70% → increase VM
👉 If CPU < 30% → decrease VM

---

## 🔹 Step 7: Load Balancer Setup

1. While creating VMSS:

   * Enable Load Balancer
2. Choose:

   * Public LB

---

## 🔹 Step 8: Test Load Balancing

1. SSH into VMs
2. Change HTML:

VM1:

```bash
echo "Server 1" > /var/www/html/index.html
```

VM2:

```bash
echo "Server 2" > /var/www/html/index.html
```

---

## 🔹 Step 9: Increase CPU (Test Scaling)

Run stress:

```bash
sudo apt install stress -y
stress --cpu 2
```

👉 Observe:

* VMSS will create new VM automatically

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

