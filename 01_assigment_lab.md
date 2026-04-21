
🎯 Lab Goal (simple)

You will create:

3 environments: Test, Staging, Production

Each has:

VNet + Subnet

1 Ubuntu VM


Connect all VNets

Setup DNS (Azure Private DNS)

Control:

Test → NOT auto discover

Staging/Prod → auto register




---

🧱 STEP 1: Login Azure

1. Go to: https://portal.azure.com


2. Login




---

🌐 STEP 2: Create VNets

🔹 Create TEST VNet

1. Search → Virtual Networks


2. Click → Create


3. Fill:

Resource group → Create new → rg-devops-lab

Name → vnet-test

Region → (same for all, e.g., East US)




👉 Next: IP Addresses

Address space: 10.0.0.0/16


👉 Subnet:

Name: subnet-test

Range: 10.0.0.0/24


👉 Click Review + Create → Create


---

🔹 Create STAGING VNet

Repeat same:

Name: vnet-staging

Address: 10.1.0.0/16

Subnet: 10.1.0.0/24



---

🔹 Create PROD VNet

Name: vnet-prod

Address: 10.2.0.0/16

Subnet: 10.2.0.0/24



---

🔗 STEP 3: VNet Peering (connect all)

Connect TEST ↔ STAGING

1. Go → vnet-test


2. Left → Peerings


3. Click → + Add



Fill:

Name: test-to-staging

Remote VNet: vnet-staging

Allow traffic: ✅


👉 Click Add

Now reverse:

Go vnet-staging → peer to vnet-test



---

Connect STAGING ↔ PROD

Same process


---

Connect TEST ↔ PROD

Same process


---

💻 STEP 4: Create Ubuntu VMs

🔹 Create TEST VM

1. Search → Virtual Machines


2. Click → Create



Fill:

Name: vm-test

Image: Ubuntu 22.04

Size: small (B1s ok)

Username: azureuser

Password: set


👉 Networking:

VNet: vnet-test

Subnet: subnet-test


👉 Create


---

🔹 Create STAGING VM

Name: vm-staging

VNet: vnet-staging



---

🔹 Create PROD VM

Name: vm-prod

VNet: vnet-prod



---

🔐 STEP 5: Allow Ping (IMPORTANT)

For ALL VMs:

1. Go VM → Networking


2. Click → Add inbound rule



Add:

Protocol: ICMP

Action: Allow



---

🌍 STEP 6: Create Private DNS

1. Search → Private DNS Zones


2. Click → Create



Fill:

Name: devops.internal

Resource group: same


👉 Create


---

🔗 STEP 7: Link VNets to DNS

Go DNS zone → Virtual network links


---

🔹 Link TEST (NO auto register)

1. Click → + Add


2. Name: link-test


3. VNet: vnet-test


4. Auto registration: ❌ OFF


5. Create




---

🔹 Link STAGING (auto register)

Name: link-staging

Auto registration: ✅ ON



---

🔹 Link PROD (auto register)

Name: link-prod

Auto registration: ✅ ON



---

🧾 STEP 8: Test DNS

Connect to VM (SSH)

From your PC:

ssh azureuser@<public-ip>


---

🔹 Check STAGING VM

From TEST VM:

ping vm-staging.devops.internal

✅ Should work (auto registered)


---

🔹 Check PROD VM

ping vm-prod.devops.internal

✅ Should work


---

🔴 TEST VM (manual DNS)

Since auto register OFF:

Go DNS Zone → + Record set

Add:

Name: vm-test

IP: (private IP of test VM)



---

Now test:

ping vm-test.devops.internal


---

✅ FINAL TEST (IMPORTANT)

From any VM:

ping vm-test.devops.internal
ping vm-staging.devops.internal
ping vm-prod.devops.internal

✔ All should work


----------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------

LAB. 2 

🔹 🔧 TASK 1: Create Infrastructure (3 VMs + 3 VNets)

✅ Step 1: Login to Azure

1. Go to 👉 Microsoft Azure Portal


2. Sign in




---

✅ Step 2: Create Resource Group

1. Click ☰ Menu (top left)


2. Click Resource groups


3. Click + Create


4. Fill:

Name: RG-Network-Lab

Region: East US



5. Click Review + Create → Create




---

✅ Step 3: Create First VNet (New York)

1. Search Virtual Networks


2. Click + Create


3. Fill:

Resource group: RG-Network-Lab

Name: VNet-NewYork

Region: East US



4. IP tab:

Address space: 10.0.0.0/16

Subnet: 10.0.1.0/24



5. Click Review + Create → Create




---

✅ Step 4: Create Second VNet (Boston - same region)

Repeat same steps:

Name: VNet-Boston

Region: East US

Address: 10.1.0.0/16

Subnet: 10.1.1.0/24



---

✅ Step 5: Create Third VNet (Seattle - different region)

Name: VNet-Seattle

Region: West US

Address: 10.2.0.0/16

Subnet: 10.2.1.0/24



---

✅ Step 6: Create Virtual Machines (3 VMs)

👉 Go to Virtual Machines → + Create

VM1 (New York)

Name: VM-NewYork

Region: East US

VNet: VNet-NewYork

Subnet: default

Image: Ubuntu

Username/password set karo

Click Review + Create → Create



---

VM2 (Boston)

Name: VM-Boston

Region: East US

VNet: VNet-Boston



---

VM3 (Seattle)

Name: VM-Seattle

Region: West US

VNet: VNet-Seattle



---

🔹 🔗 TASK 2: VNet Peering

✅ Step 7: Local Peering (Same Region)

👉 Go to VNet-NewYork

1. Left menu → Peerings


2. Click + Add



Fill:

Peering name: NY-to-Boston

Remote VNet: VNet-Boston

Allow traffic: ✅ Enabled


Click Add


---

👉 Now repeat from Boston side:

Boston-to-NY



---

✅ Step 8: Global Peering (Different Region)

👉 Go to VNet-NewYork

Peering → + Add

Name: NY-to-Seattle

Remote: VNet-Seattle


👉 Repeat from Seattle side:

Seattle-to-NY



---

🔹 🌐 TASK 3: Test Connectivity

✅ Step 9: Connect to VM

1. Go to VM (example: VM-NewYork)


2. Click Connect → SSH


3. Copy command → run in terminal




---

✅ Step 10: Test Ping

From VM-NewYork:

ping <Private-IP-of-VM-Boston>
ping <Private-IP-of-VM-Seattle>

👉 Private IP check:

VM → Networking → see private IP



---

❗ IMPORTANT (Common Error Fix)

If ping not working:

👉 Go to VM → Networking → NSG

1. Click Inbound rules


2. Click + Add


3. Allow:

Protocol: ICMP

Action: Allow





---

🎯 FINAL RESULT

✔ Same region (NY ↔ Boston) → working
✔ Different region (NY ↔ Seattle) → working


---

💡 Interview Tip (IMPORTANT)

If interviewer asks:

👉 “What is VNet Peering?” 👉 Answer:

> It connects two virtual networks so they can communicate using private IP without internet.




---

🔥 Now your turn (DevOps Question)

👉 What is difference between VNet Peering and VPN Gateway?
