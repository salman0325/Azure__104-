
# 🔹 LAB 1 GOAL

* Create **VNet + Subnets**
* Deploy **Azure Firewall**
* Create **Route Table**
* Configure **DNAT (inbound access to VM)**
* Configure **Outbound rule (VM → Internet)**
* Test both directions

---

# ⚠️ IMPORTANT BEFORE START

* Use **same region for all resources**
* Resource Group: `RG-FW-LAB`
* Subnet name for firewall **MUST be exactly**:

```id="fwsubnet"
AzureFirewallSubnet
```

---

# 🔹 STEP 1: Create Virtual Network

---

### Go to:

👉 **Microsoft Azure Portal**

---

### Click flow:

1. Click **Virtual networks**
2. Click **+ Create**

---

### Basics:

* Resource Group → **Create new**

  * Name → `RG-FW-LAB`
* Name → `VNet-FW`
* Region → same region

---

### IP Addresses:

* Address space → `10.0.0.0/16`

---

### Subnets → Click **+ Add subnet**

#### Subnet 1 (VM subnet):

* Name → `Workload-Subnet`
* Address → `10.0.1.0/24`
  👉 Click **Add**

---

#### Subnet 2 (Firewall subnet):

* Name → **AzureFirewallSubnet** (exact name)
* Address → `10.0.2.0/24`
  👉 Click **Add**

---

👉 Click:
**Review + Create → Create**

---

# 🔹 STEP 2: Create Virtual Machine

---

### Go to:

1. Virtual machines → **+ Create**

---

### Basics:

* Resource Group → `RG-FW-LAB`
* VM Name → `VM-FW`
* Region → same
* Image → Windows Server
* Size → B1s

---

### Admin:

* Username → `azureuser`
* Password → set strong

---

### Inbound Ports:

* Allow RDP (3389)

---

### Networking:

* Virtual Network → `VNet-FW`
* Subnet → `Workload-Subnet`

---

👉 Click:
**Review + Create → Create**

---

# 🔹 STEP 3: Create Public IP for Firewall

---

1. Search → **Public IP addresses**
2. Click **+ Create**

---

### Fill:

* Name → `FW-PublicIP`
* SKU → Standard
* Assignment → Static

👉 Click:
**Review + Create → Create**

---

# 🔹 STEP 4: Deploy Azure Firewall

---

1. Search → **Firewalls**
2. Click **+ Create**

---

### Basics:

* Resource Group → `RG-FW-LAB`
* Name → `AzureFirewall1`
* Region → same

---

### Firewall SKU:

* Select → **Standard**

---

### Virtual Network:

* Choose → `VNet-FW`

---

### Public IP:

* Select → `FW-PublicIP`

---

👉 Click:
**Review + Create → Create**

⏳ Wait (takes ~5–10 minutes)

---

# 🔹 STEP 5: Create Route Table

---

1. Search → **Route tables**
2. Click **+ Create**

---

### Fill:

* Name → `RT-FW`
* Resource Group → `RG-FW-LAB`

👉 Click **Create**

---

### Add Route:

1. Open `RT-FW`
2. Click **Routes → + Add**

---

### Fill:

* Route name → `DefaultRoute`
* Address prefix → `0.0.0.0/0`
* Next hop type → **Virtual appliance**
* Next hop IP → (Firewall Private IP)

👉 To get Firewall IP:

* Go to Firewall → copy **Private IP**

---

👉 Click **Add**

---

### Associate Route Table:

1. Click **Subnets → + Associate**
2. Select:

* VNet → `VNet-FW`
* Subnet → `Workload-Subnet`

👉 Click **OK**

---

# 🔹 STEP 6: Configure DNAT Rule (Inbound)

---

1. Go to **AzureFirewall1**
2. Click **Rules → NAT rules → + Add NAT rule collection**

---

### Fill:

#### Collection:

* Name → `DNAT-Rule`
* Priority → 100
* Action → DNAT

---

### Rule:

* Name → `RDP-Rule`
* Protocol → TCP
* Source → `*`
* Destination address → Firewall Public IP
* Destination port → `3389`
* Translated address → VM private IP
* Translated port → `3389`

👉 Click **Add**

---

# 🔹 STEP 7: Test Inbound Access

---

### Get Firewall Public IP:

* Go to `FW-PublicIP`

---

### Connect via RDP:

* Use Firewall Public IP

```id="rdp"
mstsc → enter FW public IP
```

👉 If working:
✔ DNAT successful
✔ You are inside VM

---

# 🔹 STEP 8: Configure Outbound Rule

---

1. Go to Firewall → **Rules**
2. Click **Network rules → + Add network rule collection**

---

### Fill:

#### Collection:

* Name → `Allow-Internet`
* Priority → 200
* Action → Allow

---

### Rule:

* Name → `Allow-Web`
* Protocol → TCP
* Source → VM subnet (`10.0.1.0/24`)
* Destination → `0.0.0.0/0`
* Destination ports → `80,443`

👉 Click **Add**

---

# 🔹 STEP 9: Test Outbound Access

---

### Connect to VM (RDP)

Open browser:

👉 Try:

* `https://www.google.com`

✔ If working:

* Outbound rule successful

---

# ❌ TROUBLESHOOTING (VERY IMPORTANT)

---

### 1. RDP not working?

* Check DNAT rule correct
* Check VM firewall (allow RDP)

---

### 2. Internet not working?

* Check Route Table attached
* Check Firewall rule (port 80/443)

---

### 3. Route issue?

* Ensure:

```id="route"
0.0.0.0/0 → Firewall Private IP
```

---

# 🔹 FINAL RESULT

✔ Inbound: Internet → Firewall → VM (DNAT)
✔ Outbound: VM → Firewall → Internet
✔ Firewall fully controlling traffic

---

# 🔹 QUICK INTERVIEW LINE

👉 “Azure Firewall controls inbound using DNAT and outbound using network/application rules with implicit deny by default.”
----------------------------------------------------------------------------------------------------------------------------



# 🔹 LAB 2 GOAL

* Create **2 VMs in different VNets**
* Connect them using **VNet Peering**
* Configure **Private DNS**
* Ping VM1 from VM2 using **name (not IP)**

---

# ⚠️ BEFORE START

Make sure:

* Same **region** (important for simplicity)
* Example region: *East US* (you can choose any)

---

# 🔹 STEP 1: Create VM1 (with VNet1)

### Go to:

👉 **Microsoft Azure Portal**

### Click flow:

1. Click **"Virtual machines"**
2. Click **"+ Create"**
3. Click **"Azure virtual machine"**

---

### Basics Tab:

* Subscription → select yours

* Resource Group → Click **"Create new"**

  * Name: `RG-LAB`
  * Click **OK**

* VM Name → `VM1`

* Region → Same for both VMs (IMPORTANT)

* Image → Windows Server 2019 (or Ubuntu if you want)

* Size → Click **"See all sizes" → Select small (B1s)**

---

### Administrator:

* Username → `azureuser`
* Password → (create strong password)

---

### Inbound Ports:

* Select → **Allow RDP (3389)** (for Windows)
* OR SSH (22) if Linux

---

### Networking Tab:

* Virtual Network → Click **"Create new"**

  * Name: `VNet1`
* Subnet → default (leave)

---

### Click:

👉 **Review + Create → Create**

⏳ Wait until deployment complete

---

# 🔹 STEP 2: Create VM2 (with VNet2)

Repeat same process but:

### Change:

* VM Name → `VM2`
* Virtual Network → Click **Create new**

  * Name → `VNet2`

👉 Keep:

* Same Resource Group (RG-LAB)
* Same Region

👉 Click:
**Review + Create → Create**

---

# 🔹 STEP 3: VNet Peering

Now connect both VNets

---

### Go to:

1. Click **Virtual networks**
2. Click **VNet1**

---

### Inside VNet1:

1. Click **"Peerings"**
2. Click **"+ Add"**

---

### Fill details:

#### This VNet (VNet1 side):

* Peering name → `VNet1-to-VNet2`

#### Remote VNet:

* Peering link name → `VNet2-to-VNet1`
* Select VNet → choose `VNet2`

---

### IMPORTANT OPTIONS (enable ALL):

✔ Allow virtual network access
✔ Allow forwarded traffic
✔ Allow gateway transit (optional)

---

👉 Click **Add**

⏳ Wait until status = **Connected**

---

# 🔹 STEP 4: Test Connectivity (IP)

---

### Get Private IPs:

1. Go to VM1 → copy **Private IP**
2. Go to VM2 → connect using **RDP**

---

### Inside VM2:

1. Open **Command Prompt**
2. Type:

```id="j0c1"
ping <VM1-private-IP>
```

👉 If working:
✔ Peering is successful

---

# 🔹 STEP 5: Create Private DNS Zone

---

### Go to:

1. Search → **Private DNS zones**
2. Click **"+ Create"**

---

### Fill:

* Resource Group → `RG-LAB`
* Name → `internal.local`

👉 Click:
**Review + Create → Create**

---

# 🔹 STEP 6: Link VNet1 to DNS

---

1. Open DNS zone → `internal.local`
2. Click **"Virtual network links"**
3. Click **"+ Add"**

---

### Fill:

* Link name → `link-vnet1`
* Virtual network → `VNet1`
* ✔ Enable **Auto registration**

👉 Click **OK**

---

# 🔹 STEP 7: Link VNet2 to DNS

---

1. Click **"+ Add"** again

### Fill:

* Link name → `link-vnet2`
* Virtual network → `VNet2`
* ✔ Enable Auto registration

👉 Click **OK**

---

# 🔹 STEP 8: Verify DNS Records

---

1. Go to DNS zone → **"Record sets"**

👉 You should see:

* VM1 record
* VM2 record

Example:

```
vm1.internal.local
vm2.internal.local
```

---

# 🔹 STEP 9: Test Name Resolution

---

### Connect to VM2 (RDP)

Open Command Prompt:

```id="p2l8"
ping vm1.internal.local
```

---

# ✅ EXPECTED RESULT

✔ Ping should work using **name (not IP)**
✔ That means DNS is working

---

# ❌ IF ERROR (VERY IMPORTANT FIXES)

### 1. Ping not working?

* Go to VM1 → **Windows Firewall**
* Turn off OR allow ICMP

---

### 2. Name not resolving?

* Wait 2–5 minutes (DNS sync delay)
* Check auto-registration is enabled

---

### 3. Peering not working?

* Check status = **Connected**
* Both VNets in same region

---

# 🔹 FINAL RESULT

✔ VM1 & VM2 connected
✔ DNS working
✔ Name-based ping successful




