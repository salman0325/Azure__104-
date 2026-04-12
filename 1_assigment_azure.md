# 🏷️ 1. Tags

### 📌 What:

👉 Tags = **key-value labels** used to organize cloud resources

---

### ❓ Why:

* Easy to manage resources
* Track cost (billing)
* Identify owner/project

---

### 💡 Example:

```
Resource: VM1
Tags:
Environment = Dev
Owner = Salman
Project = Website
```

---

### 🧠 Simple:

👉 Tags = labels on files

---

# 📈 2. Scalability

### 📌 What:

👉 Ability to **increase or decrease resources**

---

### ❓ Why:

* Handle more users
* Save cost when traffic is low

---

## 🔹 Types:

### 1. Vertical Scaling (Scale Up)

👉 Increase power of one machine

💡 Example:

* RAM 4GB → 8GB

---

### 2. Horizontal Scaling (Scale Out)

👉 Add more machines

💡 Example:

* 1 server → 3 servers

---

### 🧠 Simple:

👉 Vertical = bigger machine
👉 Horizontal = more machines

---

# 🌐 3. IP Address

### 📌 What:

👉 Unique number for every device

---

### ❓ Why:

* Communication between devices

---

### 💡 Example:

* 192.168.1.1
* 10.0.0.5

---

## 🔹 Types:

### Private IP

👉 Inside network

### Public IP

👉 Internet use

---

### 🧠 Simple:

👉 IP = home address

---

# 📊 4. CIDR Block (IMPORTANT)

### 📌 What:

👉 **CIDR = Classless Inter-Domain Routing**
👉 Used to define **IP range**

---

### ❓ Why:

* Control number of IPs
* Create subnets

---

### 💡 Example:

👉 **192.168.1.0/24**

* `/24` = subnet mask
* Total IPs = **256**

---

### 🔢 Common CIDR:

| CIDR | IPs |
| ---- | --- |
| /24  | 256 |
| /25  | 128 |
| /26  | 64  |

---

### 🧠 Simple:

👉 CIDR = size of network

---

# 🧩 5. Subnet

### 📌 What:

👉 Small network inside big network

---

### ❓ Why:

* Security
* Organization
* Traffic control

---

### 💡 Example:

👉 Network:
192.168.1.0/24

👉 Subnets:

* 192.168.1.0/26
* 192.168.1.64/26
* 192.168.1.128/26

---

### 🧠 Simple:

👉 Subnet = divide network

---

# 🔥 IP + CIDR + Subnet (Full Example)

👉 Network:
192.168.1.0/24 → 256 IPs

👉 Divide:

* Subnet1 → 192.168.1.0/26 (64 IPs)
* Subnet2 → 192.168.1.64/26
* Subnet3 → 192.168.1.128/26

---

# 🚀 NEXT WEEK TOPICS (VERY IMPORTANT)

---

# 🌐 6. VNet (Virtual Network)

### 📌 What:

👉 VNet = **private network in Azure cloud**

---

### ❓ Why:

* Secure communication
* Isolate resources

---

### 💡 Example:

👉 Create VNet:
10.0.0.0/16

Inside it:

* Subnet1 → Web
* Subnet2 → DB

---

### 🧠 Simple:

👉 VNet = your own network in cloud

---

# 🔗 7. VNet Peering

### 📌 What:

👉 Connect two VNets

---

### ❓ Why:

* Share resources
* Communication between networks

---

### 💡 Example:

* VNet1 (Web)
* VNet2 (Database)

👉 Peering → both can communicate

---

### 🧠 Simple:

👉 Peering = network connection

---

# 🌍 8. DNS (Domain Name System)

### 📌 What:

👉 Converts **name → IP**

---

### ❓ Why:

* Easy to remember names

---

### 💡 Example:

👉 google.com → 142.x.x.x

---

### 🧠 Simple:

👉 DNS = phonebook of internet

---

# 🔒 9. NSG (Network Security Group)

### 📌 What:

👉 NSG = **security rules (firewall)**

---

### ❓ Why:

* Control traffic (allow/deny)

---

### 💡 Example:

Rule:

* Allow port 80 (HTTP)
* Deny all others

---

### 🧠 Simple:

👉 NSG = gatekeeper

---

# 🔥 10. Azure Firewall

### 📌 What:

👉 Advanced cloud firewall

---

### ❓ Why:

* More security
* Central control

---

### 💡 Example:

👉 Block malicious traffic
👉 Allow only safe requests

---

### 🧠 Simple:

👉 Azure Firewall = smart security system

---

# 🧠 FINAL SUPER SIMPLE SUMMARY

👉 Tags = labels
👉 Scalability = increase/decrease resources
👉 IP = address
👉 CIDR = network size
👉 Subnet = small network

👉 VNet = cloud network
👉 Peering = connect networks
👉 DNS = name → IP
👉 NSG = basic firewall
👉 Azure Firewall = advanced firewall

