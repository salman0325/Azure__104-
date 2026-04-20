
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


