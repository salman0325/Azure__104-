
# 🔥 LAB 1 — VNet + Subnet + 2 Ubuntu VMs (FULL DETAILED)

## 🎯 Goal:

* 1 VNet create
* 2 Subnets create
* 2 Ubuntu VMs create
* Connectivity test (ping)

---

# 🟢 STEP 1: Azure Portal Login

1. Open browser
2. Go to:

```id="r6b8sx"
https://portal.azure.com
```

3. Login with your account

---

# 🟢 STEP 2: Create Resource Group (VERY IMPORTANT)

👉 Search bar (top) → type:

```
Resource groups
```

### Click:

👉 “Create”

Fill:

* Subscription: Free Tier
* Resource Group Name:

```id="8h7kqk"
my-rg
```

* Region: **UAE North** (recommended)

👉 Click:

```
Review + Create
```

👉 Click:

```
Create
```

---

# 🟢 STEP 3: Create Virtual Network (VNet)

Search:

```
Virtual networks
```

👉 Click:

```
Create
```

---

### Basics Tab:

* Subscription: Free Tier
* Resource Group: `my-rg`
* Name:

```id="k3m0n1"
myVNet
```

* Region: UAE North

👉 Click: NEXT

---

### IP Addresses Tab:

👉 Remove default if needed

Add:

```
Address Space:
10.0.0.0/16
```

---

# 🟢 STEP 4: Create Subnets

Inside same page:

👉 Click:

```
+ Add subnet
```

---

### Subnet 1:

* Name:

```id="s1a1"
subnet-1
```

* CIDR:

```
10.0.1.0/24
```

👉 Click Add

---

### Subnet 2:

* Name:

```id="s2a2"
subnet-2
```

* CIDR:

```
10.0.2.0/24
```

👉 Click Add

---

👉 Click:

```
Review + Create
```

👉 Click:

```
Create
```

---

# 🟢 STEP 5: Create Ubuntu VM #1

Search:

```
Virtual Machines
```

👉 Click:

```
Create → Azure virtual machine
```

---

### Basics Tab:

* Subscription: Free

* Resource Group: `my-rg`

* VM Name:

```id="vm1"
ubuntu-vm-1
```

* Region: UAE North

* Image:
  👉 **Ubuntu Server 22.04 LTS**

* Size:
  👉 B1s (free tier)

* Authentication:
  👉 Username: `azureuser`
  👉 Password: set strong password

---

👉 Click NEXT

---

### Networking Tab:

* Virtual Network:
  👉 `myVNet`

* Subnet:
  👉 `subnet-1`

---

👉 Click:

```
Review + Create
```

👉 Click:

```
Create
```

---

# 🟢 STEP 6: Create Ubuntu VM #2

Repeat same steps:

Search → Virtual Machines → Create

---

### Basics:

* Name:

```id="vm2"
ubuntu-vm-2
```

* Image:
  👉 Ubuntu 22.04

---

### Networking:

* VNet: `myVNet`
* Subnet: `subnet-2`

---

👉 Create VM

---

# 🟢 STEP 7: Get Private IPs

Go to:

👉 Virtual Machines
👉 Click `ubuntu-vm-1`
👉 Copy:

```
Private IP
```

Do same for VM2

---

# 🟢 STEP 8: Connect to VM (SSH)

Open terminal:

```bash id="ssh1"
ssh azureuser@<VM1-PUBLIC-IP>
```

Same for VM2

---

# 🟢 STEP 9: Enable Ping (ICMP)

## On BOTH Ubuntu VMs:

Run:

```bash id="icmp1"
sudo ufw allow icmp
sudo ufw enable
```

---

# 🟢 STEP 10: Test Connectivity

From VM1:

```bash id="ping1"
ping 10.0.2.X
```

👉 (VM2 private IP use karo)

---

# 🎉 RESULT:

✔ VNet working
✔ Subnets working
✔ VM-to-VM communication successful

---

# 🔥 LAB 2 — VNet Peering (FULL STEP)

---

## 🟢 STEP 1: Create Second VNet

Search:

```
Virtual networks
```

👉 Create:

* Name:

```id="vnet2"
myVNet2
```

* Address:

```
20.0.0.0/16
```

---

## 🟢 STEP 2: Create Subnet

* subnet:

```
20.0.1.0/24
```

---

## 🟢 STEP 3: Create Ubuntu VM

* Name:

```id="vm3"
ubuntu-vm-3
```

* VNet: myVNet2

---

## 🟢 STEP 4: Try Ping (FAIL)

👉 VM1 → VM3 ping

❌ No response

---

## 🟢 STEP 5: Create Peering

Go to:

👉 myVNet → Peering

Click:

```
+ Add
```

---

### Fill:

* Name:

```
vnet1-to-vnet2
```

* Remote VNet:

```
myVNet2
```

👉 Click OK

---

👉 Now reverse:

Go to myVNet2 → Peering → Add

---

## 🟢 STEP 6: Test Again

From VM1:

```bash id="ping2"
ping <VM3-private-ip>
```

---

🎉 SUCCESS ✔

---

# 🔥 LAB 3 — NSG Security (FULL STEP)

---

## 🟢 STEP 1: Create VM (No access initially)

Create:

* Ubuntu VM
* Name:

```id="vm4"
secure-vm
```

---

## 🟢 STEP 2: Try SSH

❌ Connection fails

---

## 🟢 STEP 3: Create NSG

Search:

```
Network Security Groups
```

👉 Create:

* Name:

```id="nsg1"
my-nsg
```

---

## 🟢 STEP 4: Add Rule

Go to NSG → Inbound Rules → Add

---

### Fill:

* Source: IP Addresses
* Source IP: YOUR PUBLIC IP
* Destination: Any
* Port: 22
* Protocol: TCP
* Action: Allow
* Priority: 100
* Name: allow-ssh

---

## 🟢 STEP 5: Attach NSG

Go VM:

👉 secure-vm
👉 Networking
👉 Attach NSG → `my-nsg`

---

## 🟢 STEP 6: Test SSH

```bash id="ssh2"
ssh azureuser@<public-ip>
```

---

🎉 NOW WORKING ✔

---

# 🔥 FINAL SIMPLE UNDERSTANDING

* VNet = Network
* Subnet = Division
* VM = Machine
* ICMP = Ping test
* Peering = Network connection
* NSG = Firewall

