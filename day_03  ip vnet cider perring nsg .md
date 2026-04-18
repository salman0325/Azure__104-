Theek hai 👍 — main tumhara content **clean English + proper definitions + examples** mein rewrite kar raha hoon, aur **lab skip** kar raha hoon jaise tum ne bola.

---

# 🔥 1. IP Address

## 🔹 What is IP Address?

An **IP address (Internet Protocol address)** is a **unique numerical identifier** assigned to every device on a network.

👉 It helps devices communicate with each other.

### Example:

```
192.168.1.10
```

---

## 🔹 IPv4 Structure

IPv4 is a **32-bit address**, divided into 4 parts (called octets):

```
192.168.1.10
```

Each part = 8 bits

---

## 🔹 Why IP is needed?

* Identify device on network
* Send/receive data
* Enable communication between systems

---

# 🔥 2. IP Classes (Classful Addressing)

👉 Old system used to divide IPs into classes.

---

## 🔸 Class A

* Range: 1.0.0.0 – 126.255.255.255
* Default mask: 255.0.0.0
* Use: Very large networks

### Example:

```
10.0.0.0
```

---

## 🔸 Class B

* Range: 128.0.0.0 – 191.255.255.255
* Mask: 255.255.0.0
* Use: Medium networks

---

## 🔸 Class C

* Range: 192.0.0.0 – 223.255.255.255
* Mask: 255.255.255.0
* Use: Small networks

---

## 🔸 Class D

* Range: 224.0.0.0 – 239.255.255.255
* Use: Multicast (video streaming, group communication)

---

## 🔸 Class E

* Range: 240.0.0.0 – 255.255.255.255
* Use: Research (not public use)

---

# 🔥 3. CIDR (Classless Inter-Domain Routing)

## 🔹 What is CIDR?

CIDR is a modern method of IP allocation that removes fixed classes and allows flexible subnetting.

---

## 🔹 Example:

```
192.168.1.0/24
```

👉 `/24` means:

* 24 bits = network part
* 8 bits = host part

---

## 🔹 Formula:

```
Total IPs = 2^(32 - prefix)
```

---

## 🔹 Example:

```
10.0.0.0/16
```

```
2^(32-16) = 65,536 IP addresses
```

---

# 🔥 4. Public vs Private IP

## 🔹 Public IP

A public IP is **accessible over the internet**.

---

## 🔹 Private IP

A private IP is used **inside a local network only** and cannot be accessed directly from the internet.

---

## 🔹 Private IP Ranges:

```
10.0.0.0 – 10.255.255.255   (/8)
172.16.0.0 – 172.31.255.255 (/12)
192.168.0.0 – 192.168.255.255 (/16)
```

---

# 🔥 5. Azure Virtual Network (VNet)

## 🔹 What is VNet?

Microsoft Azure Virtual Network (VNet) is a **private network in Azure** that allows Azure resources (like Virtual Machines) to communicate securely.

---

## 🔹 Definition:

A VNet is a **logically isolated network in Azure** where you can run and manage your cloud resources securely.

---

## 🔹 Example:

```
VNet: 10.0.0.0/16
```

Inside it:

* Subnet-1: 10.0.1.0/24
* Subnet-2: 10.0.2.0/24

---

## 🔹 Key Components:

### 1. Address Space

Defines the IP range of VNet.

Example:

```
10.0.0.0/16
```

---

### 2. Subnet

A **smaller division of VNet** used to organize resources.

Example:

```
10.0.1.0/24
```

---

### 3. VNIC (Virtual Network Interface Card)

A virtual network card attached to a VM for connectivity.

---

# 🔥 6. Azure Reserved IPs

In each subnet, Azure reserves **5 IP addresses**:

| Purpose   | Description     |
| --------- | --------------- |
| Network   | First IP        |
| Gateway   | Default gateway |
| DNS       | Azure DNS       |
| Future    | Reserved        |
| Broadcast | Last IP         |

---

# 🔥 7. ICMP (Ping Protocol)

## 🔹 What is ICMP?

ICMP (Internet Control Message Protocol) is used for **network testing (ping command)**.

---

## 🔹 In Azure:

* ICMP is **blocked by default**
* Must be manually allowed using firewall/NSG rules

---

# 🔥 8. VNet Peering

## 🔹 What is VNet Peering?

VNet Peering allows **two Azure VNets to connect directly** using Microsoft’s backbone network.

---

## 🔹 Definition:

A secure, private connection between two VNets enabling communication between resources.

---

## 🔹 Types:

### 1. Regional Peering

* Same region
* Low cost
* High speed

### 2. Global Peering

* Different regions
* Higher cost
* Global connectivity

---

## 🔹 Important Rule:

❌ Peering is **NOT transitive**

Example:

* A ↔ B
* B ↔ C
  👉 A cannot automatically reach C

---

# 🔥 9. NSG (Network Security Group)

Azure Network Security Group is a **virtual firewall in Azure** that controls traffic to and from Azure resources.

---

## 🔹 Definition:

NSG is a **layer 3 & layer 4 firewall** used to allow or deny network traffic.

---

## 🔹 Stateful Firewall:

* If request is allowed → response automatically allowed

---

## 🔹 Rule Priority:

* Range: 100 – 4096
* Lower number = higher priority

Example:

```
100 → Allow SSH
200 → Deny all
```

---

## 🔹 NSG Levels:

* Subnet NSG (applies to all resources in subnet)
* NIC NSG (applies to specific VM)

👉 NIC rule overrides subnet rule

---

# 🔥 10. Azure Firewall

Azure Firewall is a **managed, advanced network security service** that provides centralized control over traffic filtering.

---

## 🔹 Difference from NSG:

| NSG            | Azure Firewall    |
| -------------- | ----------------- |
| Basic firewall | Advanced firewall |
| Per subnet/VM  | Central control   |
| L3/L4          | L3–L7 filtering   |

---

# 🔥 FINAL SUMMARY (Easy Revision)

* IP = Device identity
* Class A/B/C = old IP system
* CIDR = modern flexible IP system
* VNet = Azure private network
* Subnet = VNet division
* ICMP = ping protocol
* NSG = firewall for traffic control
* Peering = connect two VNets
* Azure Firewall = advanced security system
