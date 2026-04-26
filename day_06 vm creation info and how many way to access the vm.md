🔷 1. VM Pricing Models
✅ Pay-As-You-Go
You pay only for what you use
Good for testing or short-term work

✅ Reserved (1–3 years)
You commit for long time
Much cheaper

✅ Spot VM
Very cheap
Azure can stop it anytime

🔷 2. VM Sizes & Types
VM size means:
CPU (power)
RAM (memory)

Common types:
B-Series → cheap, small work
D-Series → normal usage
E-Series → high memory
F-Series → high CPU

🔷 3. Storage Types
Disk types:
Standard HDD → slow, cheap
Standard SSD → better
Premium SSD → fast
Ultra Disk → very fast (expensive)

🔷 4. VM Creation Options (Important)

When creating VM:

Region → where VM is located
Image → OS (Linux / Windows)
Size → performance
Authentication → password or SSH key
Public IP → internet access
NSG (Firewall) → allow ports like SSH (22)

👉 Why check these?
Security
Cost control
Performance

🔷 5. Tiers (Basic / Standard / Premium)
Basic → testing
Standard → normal production
Premium → high performance

🔷 6. How to Connect to VM (3 ways)

✅ 1. Public IP
Direct connection from internet

✔ Easy
❌ Not secure

✅ 2. Jumpbox (Bastion Host VM)
One VM with public IP
Use it to access other VMs

✔ More secure
❌ Extra setup

✅ 3. Azure Bastion
Connect from browser
No public IP needed

✔ Very secure
❌ Costly

🔷 7. VM Troubleshooting (if not connecting)

Check:
VM is running
Port 22/3389 open
Correct IP
Username/password
Restart VM

🔷 8. Azure Bastion
Secure access using browser
No need for public IP

🔷 9. Azure Lock
Protect resource

Types:
ReadOnly → cannot change
Delete → cannot delete

🔷 10. High Availability (HA)
VM should stay running always
No downtime

🔷 11. Fault Tolerance
System keeps working even if one part fails

🔷 12. No Infrastructure Redundancy
Only 1 VM
If it fails → everything stops

🔷 13. Availability Set

Used to protect VMs

Concepts:
Fault Domain (FD) → different hardware
Update Domain (UD) → update groups

Example:
FD = 2
UD = 5

🔷 14. Availability Zone
Different physical data centers
More protection

---

🔥 LAB: Create Jumpbox + Private VM + Access (FULL STEPS)

🧪 PART 1: Login & Start

1. Open browser
2. Go to: [https://portal.azure.com](https://portal.azure.com)
3. Login with your account

🧪 PART 2: Create Resource Group

1. Search: Resource groups
2. Click + Create
3. Fill:
   Resource group name: rg-lab
   Region: (choose nearest)
4. Click Review + Create
5. Click Create

🧪 PART 3: Create Virtual Network

1. Search: Virtual networks
2. Click + Create

Basics tab:
Resource group: rg-lab
Name: vnet-lab
Region: same

IP Addresses tab:
Leave default (10.0.0.0/16)

Subnet:
Name: subnet1
Range: 10.0.0.0/24

Click Review + Create → Create

🧪 PART 4: Create Jumpbox VM

1. Search: Virtual Machines
2. Click + Create → Azure Virtual Machine

Basics tab:
Resource group: rg-lab
VM name: jumpbox-server
Region: same
Image: Ubuntu Server 22.04
Size: B1s

Administrator account:
Username: azureuser
Authentication: Password or SSH
Enter password

Inbound ports:
Allow SSH (22)

Networking tab:
Virtual network: vnet-lab
Subnet: subnet1
Public IP: Create new (Enable)

Click Review + Create → Create

🧪 PART 5: Create Private VM

Basics:
Name: private-vm
Same resource group
Same region
Same image
Same size

Networking tab:
Virtual network: vnet-lab
Subnet: subnet1
Public IP: None (Disable)

Click Review + Create → Create

🧪 PART 6: Connect to Jumpbox

Go to Virtual Machines
Click jumpbox-server
Click Connect → SSH

Command:
ssh azureuser@<public-ip>

🧪 PART 7: Get Private VM IP

Open private-vm
Go to Networking
Copy Private IP (example: 10.0.0.5)

🧪 PART 8: Connect Private VM via Jumpbox

Inside jumpbox:
ssh azureuser@10.0.0.5

✔ Done

🔥 OPTIONAL

If SSH fails:
sudo apt update
sudo apt install openssh-client -y

🔷 TROUBLESHOOTING

Check NSG → port 22 allowed
Check VM running
Check correct IP

🔷 AVAILABILITY SET LAB

Step 1: Create Availability Set
Search Availability Sets → + Create

Name: avset-lab
Resource group: rg-lab
Fault Domains: 2
Update Domains: 5

Step 2: Create 2 VMs in Availability Set
Select Availability Set → avset-lab

Create: vm1, vm2

Step 3: Verify
Check different FD and UD

🔷 AZURE BASTION

Create Bastion
Search Bastion → + Create

Name: bastion-lab
VNet: vnet-lab
Public IP: create new

Use Bastion
Go to VM → Connect → Bastion
Enter username/password

🔷 AZURE LOCK

Go to VM → Locks → + Add

Delete → cannot delete
ReadOnly → cannot modify
