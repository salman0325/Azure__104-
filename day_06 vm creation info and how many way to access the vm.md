Alright — I’ll explain everything in **simple, easy English** step by step, no complicated wording 👍

---

# 🔷 1. VM Pricing Models

### ✅ Pay-As-You-Go

* You pay only for what you use
* Good for testing or short-term work

### ✅ Reserved (1–3 years)

* You commit for long time
* Much cheaper

### ✅ Spot VM

* Very cheap
* Azure can stop it anytime

---

# 🔷 2. VM Sizes & Types

### VM size means:

* CPU (power)
* RAM (memory)

### Common types:

* **B-Series** → cheap, small work
* **D-Series** → normal usage
* **E-Series** → high memory
* **F-Series** → high CPU

---

# 🔷 3. Storage Types

### Disk types:

* Standard HDD → slow, cheap
* Standard SSD → better
* Premium SSD → fast
* Ultra Disk → very fast (expensive)

---

# 🔷 4. VM Creation Options (Important)

When creating VM:

* **Region** → where VM is located
* **Image** → OS (Linux / Windows)
* **Size** → performance
* **Authentication** → password or SSH key
* **Public IP** → internet access
* **NSG (Firewall)** → allow ports like SSH (22)

👉 Why check these?

* Security
* Cost control
* Performance

---

# 🔷 5. Tiers (Basic / Standard / Premium)

* **Basic** → testing
* **Standard** → normal production
* **Premium** → high performance

---

# 🔷 6. How to Connect to VM (3 ways)

## ✅ 1. Public IP

* Direct connection from internet

✔ Easy
❌ Not secure

---

## ✅ 2. Jumpbox (Bastion Host VM)

* One VM with public IP
* Use it to access other VMs

✔ More secure
❌ Extra setup

---

## ✅ 3. Azure Bastion

* Connect from browser
* No public IP needed

✔ Very secure
❌ Costly

---

# 🔷 7. VM Troubleshooting (if not connecting)

Check:

1. VM is running
2. Port 22/3389 open
3. Correct IP
4. Username/password
5. Restart VM

---

# 🔷 8. Azure Bastion

* Secure access using browser
* No need for public IP

---

# 🔷 9. Azure Lock

* Protect resource

Types:

* ReadOnly → cannot change
* Delete → cannot delete

---

# 🔷 10. High Availability (HA)

* VM should stay running always
* No downtime

---

# 🔷 11. Fault Tolerance

* System keeps working even if one part fails

---

# 🔷 12. No Infrastructure Redundancy

* Only 1 VM
* If it fails → everything stops

---

# 🔷 13. Availability Set

Used to protect VMs

### Concepts:

* **Fault Domain (FD)** → different hardware
* **Update Domain (UD)** → update groups

Example:

* FD = 2
* UD = 5

---

# 🔷 14. Availability Zone

* Different physical data centers
* More protection

-------------------------------------------------------------------------------------------------------------------------------


# 🔥 LAB: Create Jumpbox + Private VM + Access (FULL STEPS)

---

# 🧪 PART 1: Login & Start

1. Open browser
2. Go to: [https://portal.azure.com](https://portal.azure.com)
3. Login with your account

---

# 🧪 PART 2: Create Resource Group

1. Search: **Resource groups**
2. Click **+ Create**
3. Fill:

   * Resource group name: `rg-lab`
   * Region: (choose nearest)
4. Click **Review + Create**
5. Click **Create**

---

# 🧪 PART 3: Create Virtual Network

1. Search: **Virtual networks**
2. Click **+ Create**

### Basics tab:

* Resource group: `rg-lab`
* Name: `vnet-lab`
* Region: same

### IP Addresses tab:

* Leave default (10.0.0.0/16)

### Subnet:

* Name: `subnet1`
* Range: 10.0.0.0/24

Click **Review + Create → Create**

---

# 🧪 PART 4: Create Jumpbox VM

1. Search: **Virtual Machines**
2. Click **+ Create → Azure Virtual Machine**

### Basics tab:

* Resource group: `rg-lab`
* VM name: `jumpbox-server`
* Region: same
* Image: Ubuntu Server 22.04
* Size: B1s (cheap)

### Administrator account:

* Username: `azureuser`
* Authentication: Password or SSH
* Enter password

---

### Inbound ports:

* Select: **Allow SSH (22)**

---

### Networking tab:

* Virtual network: `vnet-lab`
* Subnet: `subnet1`
* Public IP: **Create new (Enable)**

---

Click:
👉 Review + Create
👉 Create

⏳ Wait for deployment

---

# 🧪 PART 5: Create Private VM

Repeat VM creation:

### Basics:

* Name: `private-vm`
* Same resource group
* Same region
* Same image
* Same size

---

### Networking tab:

* Virtual network: `vnet-lab`
* Subnet: `subnet1`
* Public IP: ❌ **None (Disable)**

---

Click:
👉 Review + Create
👉 Create

---

# 🧪 PART 6: Connect to Jumpbox

1. Go to **Virtual Machines**
2. Click `jumpbox-server`
3. Click **Connect → SSH**
4. Copy command

Example:

```bash id="c1"
ssh azureuser@<public-ip>
```

---

# 🧪 PART 7: Get Private VM IP

1. Open `private-vm`
2. Go to **Networking**
3. Copy **Private IP** (example: 10.0.0.5)

---

# 🧪 PART 8: Connect Private VM via Jumpbox

Inside jumpbox:

```bash id="c2"
ssh azureuser@10.0.0.5
```

✔ Done — now you are inside private VM

---

# 🔥 OPTIONAL (Important Real Step)

If SSH fails:

### Install SSH client in jumpbox:

```bash id="c3"
sudo apt update
sudo apt install openssh-client -y
```

---

# 🔷 TROUBLESHOOTING

If not connecting:

### Check NSG:

1. Go to VM → Networking
2. Ensure port 22 is allowed

---

### Check VM status:

* Running hona chahiye

---

### Check IP:

* Public IP correct
* Private IP correct

---

# 🔷 AVAILABILITY SET LAB

---

## 🧪 Step 1: Create Availability Set

1. Search: **Availability Sets**
2. Click **+ Create**

Fill:

* Name: `avset-lab`
* Resource group: `rg-lab`
* Fault Domains: 2
* Update Domains: 5

Click:
👉 Review + Create → Create

---

## 🧪 Step 2: Create 2 VMs in Availability Set

While creating VM:

### Basics tab:

* Availability options:
  👉 Select: **Availability Set**
  👉 Choose: `avset-lab`

Create:

* vm1
* vm2

---

## 🧪 Step 3: Verify

1. Open both VMs
2. Check:

   * Different Fault Domain
   * Different Update Domain

✔ Means high availability working

----------------------------------------------
BASTION LAB 


# 🧪 COMPLETE STEP-BY-STEP (NO CONFUSION)

## 🟢 STEP 1: Create VNet (VERY IMPORTANT)

👉 Azure Portal → **Virtual Networks** → **+ Create**

Fill:

* **Name**: `vnet-lab`
* **Region**: same rakho sab ka
* Address space: default (leave)

### 🔽 Subnets tab pe:

👉 Yahan 2 subnet banana MUST hai:

### 1️⃣ VM subnet

* Name: `subnet-vm`
* Address: default (leave)

### 2️⃣ Bastion subnet (IMPORTANT ⚠️)

* Name: **AzureBastionSubnet** (exact same naam hona chahiye)
* Size: `/26` ya bada (Azure requirement)

👉 Save → Create

---

## 🟢 STEP 2: Create VM (IMPORTANT SETTINGS)

👉 Go to **Virtual Machines** → **+ Create**

### 🔹 Basics tab:

* Name: `vm-lab`
* Image: Ubuntu
* Username: `azureuser`
* Password: (ya SSH key)

---

### 🔹 Networking tab (YAHAN LOG GALTI KARTE HAIN)

* VNet: `vnet-lab` ✅
* Subnet: `subnet-vm` ✅

### ❗ Public IP:

👉 **Yes, create kar sakte ho (optional)**

✔ If beginner → **Public IP ON rakho**
✔ Advanced (secure setup) → OFF bhi kar sakte ho (Bastion ke liye enough hai)

---

### 🔹 Other options:

* NSG: default rehne do
* Ports:

  * SSH (22) → allow (agar public IP use kar rahe ho)

👉 Click **Review + Create**

---

## 🟢 STEP 3: Create Bastion

👉 Search: **Bastion** → **+ Create**

Fill:

* Name: `bastion-lab`
* Region: SAME as VM
* VNet: `vnet-lab` ✅

### 🔹 Subnet:

👉 Automatically pick karega:

* **AzureBastionSubnet** (jo tumne banaya)

---

### 🔹 Public IP:

👉 **New create karo (REQUIRED)**

* Name: `bastion-ip`

👉 Click **Create**

---

## 🟢 STEP 4: Connect using Bastion

👉 Go to your VM (`vm-lab`)

* Click: **Connect**
* Select: **Bastion**
* Enter:

  * Username
  * Password / SSH key

👉 Click **Connect**

✅ Browser ke andar SSH open ho jayega
👉 No need for public IP / no SSH client required

---

# 🔥 FINAL CONFUSION CLEAR

## ❓ VM pe Public IP zaroori hai?

| Case                    | Answer         |
| ----------------------- | -------------- |
| Bastion use kar rahe ho | ❌ Not required |
| Direct SSH karna hai    | ✅ Required     |

---

## ❓ Bastion ke liye kya zaroori hai?

* ✅ VNet same
* ✅ Subnet name: **AzureBastionSubnet**
* ✅ Public IP for Bastion

---

## 💡 Simple rule yaad rakho:

👉 **“VM private ho sakti hai, lekin Bastion ko public IP chahiye hota hai.”**



# 🔷 AZURE LOCK

---

## 🧪 Apply Lock

1. Go to any VM
2. Click **Locks**
3. Click **+ Add**

Choose:

* Delete → cannot delete
* ReadOnly → cannot modify

---
