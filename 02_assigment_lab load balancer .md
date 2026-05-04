# 🔥 ASSIGNMENT 1: Internal Load Balancer (ILB)

---

## 🎯 Goal

* 2 VMs (private)
* Internal Load Balancer
* Test via private IP (not internet)

---

# 🧪 STEP 1: Create Resource Group

1. Go to **Azure Portal**
2. Click **Resource Groups**
3. Click **+ Create**
4. Enter:

   * Name: `rg-ilb-lab`
   * Region: same for all resources
5. Click **Review + Create → Create**

---

# 🧪 STEP 2: Create VNet

1. Go to **Virtual Networks**
2. Click **+ Create**

---

### Basics:

* Name: `vnet-ilb`
* Address space:

```
10.2.0.0/16
```

---

### Subnet:

* Name: `default`
* Range:

```
10.2.1.0/24
```

👉 Click **Create**

---

# 🧪 STEP 3: Create Availability Set

1. Search → **Availability Sets**
2. Click **Create**

---

### Fill:

* Name: `avset-ilb`
* Fault domains: 2
* Update domains: 5

👉 Click Create

---

# 🧪 STEP 4: Create VM1

1. Go → **Virtual Machines → Create**

---

### Fill:

* Name: `vm1-ilb`
* Image: Ubuntu
* Availability option → **Availability Set**
* Select: `avset-ilb`
* VNet: `vnet-ilb`
* Public IP: **Disable ❗**

👉 Create

---

# 🧪 STEP 5: Create VM2

Same as VM1:

* Name: `vm2-ilb`
* Same availability set
* No public IP

---

# 🧪 STEP 6: Connect to VMs

👉 Since no public IP:

Use:

* Azure Bastion OR
* Temporary Public IP (then remove)

---

# 🧪 STEP 7: Install Nginx

### VM1:

```bash
sudo apt update
sudo apt install nginx -y
echo "Internal VM1" | sudo tee /var/www/html/index.html
```

---

### VM2:

```bash
sudo apt update
sudo apt install nginx -y
echo "Internal VM2" | sudo tee /var/www/html/index.html
```

---

# 🧪 STEP 8: Create Internal Load Balancer

1. Search → **Load Balancer → Create**

---

### Basics:

* Name: `ilb`
* Type: **Internal**
* SKU: Standard

---

### Frontend IP:

* Private IP:

```
10.2.1.100
```

👉 Click Next → Create

---

# 🧪 STEP 9: Backend Pool

1. Open ILB
2. Click **Backend pools → Add**
3. Add:

   * vm1-ilb
   * vm2-ilb

---

# 🧪 STEP 10: Health Probe

1. Click **Health probes → Add**

---

### Fill:

* Protocol: HTTP
* Port: 80
* Path: `/`

---

# 🧪 STEP 11: Load Balancing Rule

1. Click **Load balancing rules → Add**

---

### Fill:

* Frontend IP: 10.2.1.100
* Port: 80
* Backend pool: select
* Probe: select

---

# 🧪 STEP 12: Test ILB

👉 From another VM inside same VNet:

```bash
curl http://10.2.1.100
```

---

## ✅ Output:

* Internal VM1
* Internal VM2

✔ Means working

---

# ⚠️ Common Issues

* NSG blocking port 80
* No connectivity (wrong subnet)

---

# 🔥 ASSIGNMENT 2: Zone-Redundant Load Balancer

---

## 🎯 Goal

* High availability across AZ
* If 1 zone fails → app still runs

---

# 🧪 STEP 1: Create VNet

Same as before:

* Name: `vnet-zonal`
* Address:

```
10.3.0.0/16
```

---

# 🧪 STEP 2: Create VM1 (Zone 1)

1. Create VM

---

### Fill:

* Name: `vm-zone1`
* Availability option: **Availability Zone**
* Zone: **Zone 1**
* VNet: `vnet-zonal`

---

# 🧪 STEP 3: Create VM2 (Zone 2)

* Name: `vm-zone2`
* Zone: **Zone 2**

---

# 🧪 STEP 4: Install Nginx

---

### VM1:

```bash
sudo apt install nginx -y
echo "Zone 1 VM" | sudo tee /var/www/html/index.html
```

---

### VM2:

```bash
sudo apt install nginx -y
echo "Zone 2 VM" | sudo tee /var/www/html/index.html
```

---

# 🧪 STEP 5: Create Zone-Redundant Load Balancer

1. Go → Load Balancer → Create

---

### Fill:

* Name: `lb-zone`
* Type: Public
* SKU: Standard

---

### Frontend IP:

* Public IP → Create new

👉 IMPORTANT:

* Availability zone: **Zone-redundant (No zone selected)**

✔ This makes LB zone-redundant

---

# 🧪 STEP 6: Backend Pool

Add:

* vm-zone1
* vm-zone2

---

# 🧪 STEP 7: Health Probe

* HTTP
* Port 80

---

# 🧪 STEP 8: Rule

* Port 80 → 80

---

# 🧪 STEP 9: Test

Open browser:

👉 Public IP of LB

---

## ✅ Output:

* Zone 1 VM
* Zone 2 VM

---

# 🧪 STEP 10: Failure Test

👉 Stop VM in Zone 1

---

✔ Result:

* Still working (Zone 2 serving traffic)

---

# 🔥 Final Comparison

| Feature | Internal LB  | Zone-Redundant LB |
| ------- | ------------ | ----------------- |
| Access  | Private      | Public            |
| HA      | Within VNet  | Across zones      |
| Use     | Backend apps | Production apps   |

---

# 🚀 Pro Tips (Exam + Real World)

* Internal LB → Microservices backend
* Zone LB → High availability apps
* Always use **Standard SKU**
* Always configure **Health Probe**

