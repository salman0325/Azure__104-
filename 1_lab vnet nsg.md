# 🔥 1. IP Address (Deep but Easy)

## 🔹 IP Address kya hota hai?

IP address ek **unique number** hota hai jo har device ko diya jata hai network mein.

Example:

```
192.168.1.10
```

👉 IPv4 = 32 bits
👉 4 octets (8 + 8 + 8 + 8)

---

## 🔹 Binary samajh lo (basic)

```
192 = 11000000
168 = 10101000
```

---

# 🔹 Classful IP (Old Concept – Theory ke liye important)

## 🔸 Class A

* Range: 1 – 126
* Default mask: `255.0.0.0`
* Use: Large companies

👉 Example:

```
10.0.0.0
```

---

## 🔸 Class B

* Range: 128 – 191
* Mask: `255.255.0.0`
* Medium networks

---

## 🔸 Class C

* Range: 192 – 223
* Mask: `255.255.255.0`
* Small networks

---

## 🔸 Class D

* Multicast (video streaming)

## 🔸 Class E

* Research only

---

# 🔥 2. CIDR (IMPORTANT – Real World)

## 🔹 CIDR kya hai?

Old classes remove karke flexible system banaya gaya.

Example:

```
192.168.1.0/24
```

👉 `/24` = 24 bits network
👉 Remaining = host

---

## 🔹 Formula:

Total IP:

```
2^(32 - prefix)
```

---

## 🔹 Example:

`10.0.0.0/16`

```
2^(32-16) = 2^16 = 65536 IPs
```

---

## 🔹 Subnet Example:

| Subnet      | IP Range |
| ----------- | -------- |
| 10.0.1.0/24 | 256      |
| 10.0.2.0/24 | 256      |

---

# 🔥 3. Private vs Public IP

## 🔹 Public IP

* Internet pe accessible

## 🔹 Private IP

* Internal use only

Ranges:

```
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

---

# 🔥 4. Azure VNet Concepts

## 🔹 VNet kya hai?

Azure ka **private network**

👉 Sab VM, DB isi mein hote hain

---

## 🔹 Address Space

* IP range jo tum define karte ho

Example:

```
10.0.0.0/16
```

---

## 🔹 Subnet

* VNet ka chhota part

👉 Security + organization ke liye

---

## 🔹 VNIC

* VM ka network card

---

## 🔹 Azure Reserved IP

Azure har subnet mein **5 IP reserve karta hai**:

| Number | Use       |
| ------ | --------- |
| 1      | Network   |
| 2      | Gateway   |
| 3      | DNS       |
| 4      | Future    |
| 5      | Broadcast |

---

# 🔥 5. ICMP (Ping)

## 🔹 ICMP kya hai?

* Protocol jo ping ke liye use hota hai

---

## 🔹 Azure default:

❌ Block hota hai

---

## 🔹 Allow kaise kare?

### Ubuntu:

```bash
sudo ufw allow icmp
```

### Windows:

* Firewall rule allow karo

---

# 🔥 6. VNet Peering

## 🔹 Kya hota hai?

2 VNets ko directly connect karna

---

## 🔹 Important:

✔ Fast (Azure backbone)
✔ Private communication

---

## 🔹 Types:

### 1. Regional

* Same region
* Cheap

### 2. Global

* Different region
* Expensive

---

## 🔹 Not Transitive

A → B
B → C

❌ A → C automatically nahi

---

# 🔥 7. NSG (Firewall)

## 🔹 Kya hai?

Layer 3 + Layer 4 firewall

---

## 🔹 Stateful vs Stateless

| Type      | Meaning          |
| --------- | ---------------- |
| Stateful  | Reply auto allow |
| Stateless | Manual rule      |

👉 NSG = Stateful

---

## 🔹 Rule Priority

* Range: 100 – 4096
* Lower = high priority

---

## 🔹 Example:

| Priority | Rule      |
| -------- | --------- |
| 100      | Allow SSH |
| 200      | Deny All  |

---

## 🔹 Subnet vs NIC

👉 Rule conflict:

* Subnet = Allow
* NIC = Deny

👉 Final: ❌ Deny

---

# 🔥 8. Azure Firewall

* Advanced firewall
* Central control
* More secure than NSG

---

# 🔥 LAB 1 (VNet + Subnet + VM)

## 🎯 Goal:

* 1 VNet
* 2 Subnets
* 2 VM (Ubuntu + Windows)

---

## 🧭 Step-by-Step:

### 🔹 Step 1: Create VNet

1. Azure Portal open karo
2. Search → Virtual Networks
3. Click → Create

Fill:

* Name: `myVNet`
* Region: same select karo
* Address space: `10.0.0.0/16`

---

### 🔹 Step 2: Create Subnets

Add:

1. subnet-1

   * `10.0.1.0/24`

2. subnet-2

   * `10.0.2.0/24`

---

### 🔹 Step 3: Create Ubuntu VM

* Go → Virtual Machines → Create

Fill:

* Name: ubuntu-vm
* Image: Ubuntu 22.04
* Username/password

Network:

* VNet: myVNet
* Subnet: subnet-1

---

### 🔹 Step 4: Create Windows VM

* Name: windows-vm
* Subnet: subnet-2

---

### 🔹 Step 5: Enable ICMP

### Windows:

* Control Panel → Firewall → Allow ICMP

### Ubuntu:

```bash
sudo ufw allow icmp
```

---

### 🔹 Step 6: Test

```bash
ping <windows-private-ip>
```

---

# 🔥 LAB 2 (VNet Peering)

## 🎯 Goal:

* 2 VNets connect

---

## Steps:

### 🔹 Step 1: Create VNets

* VNet1 → `10.0.0.0/16`
* VNet2 → `20.0.0.0/16`

---

### 🔹 Step 2: Create VM in both

---

### 🔹 Step 3: Ping

❌ Fail (no connection)

---

### 🔹 Step 4: Peering

1. Go → VNet1
2. Click → Peering
3. Add → select VNet2

Repeat reverse

---

### 🔹 Step 5: Test

✅ Ping works

---

# 🔥 LAB 3 (NSG Security)

## 🎯 Goal:

* Restrict access

---

## Steps:

### 🔹 Step 1: Create VM

👉 No ICMP allow

---

### 🔹 Step 2: Test

❌ Ping fail

---

### 🔹 Step 3: Create NSG

* Go → NSG → Create

---

### 🔹 Step 4: Add Rule

* Source: Your IP
* Protocol: TCP
* Port: 22
* Action: Allow
* Priority: 100

---

### 🔹 Step 5: Attach NSG

* VM → Network Interface → Attach NSG

---

### 🔹 Step 6: Test

✅ Only your IP can connect

---


