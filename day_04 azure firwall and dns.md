# 🔹 Azure Firewall

**Azure Firewall**

👉 **Definition (Interview):**
Azure Firewall is a **cloud-based, fully managed network security service** that protects Azure resources by controlling inbound and outbound traffic.

👉 **Key Points:**

* PaaS service (managed by Microsoft)
* Stateful firewall (tracks connections)
* Works with rules (DNAT, Network, Application)

---

# 🔹 DNAT

👉 **Full Form:**
**Destination Network Address Translation**

👉 **Definition:**
DNAT is used to **translate a public IP address into a private IP address**.

👉 **Example:**

* Public IP → 20.1.1.1
* Private VM → 10.0.0.4
* Request goes:
  Internet → 20.1.1.1 → converted → 10.0.0.4

👉 **Use:**

* Access VM from internet (RDP/SSH/Web)

---

# 🔹 Types of Azure Firewall Rules

### 1. DNAT Rule

* Inbound traffic
* Public → Private mapping

### 2. Network Rule

* Works on IP, Port, Protocol
* Example: Allow port 80

### 3. Application Rule

* Works on domain (FQDN)
* Example: allow `www.google.com`

---

# 🔹 Implicit Deny

👉 **Definition:**
If traffic does not match any rule, it is **automatically blocked**.

👉 **Key Point:**

* Default action = Deny All

---

# 🔹 Azure Marketplace

**Azure Marketplace**

👉 **Definition:**
Azure Marketplace is an **online store** where you can deploy pre-built applications and services.

👉 **Examples:**

* Virtual Machines
* Firewalls
* Databases

---

# 🔹 SKU

👉 **Full Form:**
**Stock Keeping Unit**

👉 **Definition:**
SKU defines the **pricing tier, performance, and features** of a service.

👉 **Example (Azure Firewall):**

* Basic
* Standard
* Premium

---

# 🌐 Networking Concepts

---

# 🔹 DNS

**Domain Name System**

👉 **Full Form:**
Domain Name System

👉 **Definition:**
DNS translates **domain names into IP addresses**.

👉 **Example:**

* `www.example.com → 93.184.216.34`

---

# 🔹 ISP

👉 **Full Form:**
Internet Service Provider

👉 **Definition:**
A company that provides internet access.

👉 **Example:**

* PTCL, Nayatel

---

# 🔹 FQDN

👉 **Full Form:**
Fully Qualified Domain Name

👉 **Definition:**
Complete domain name that specifies exact location.

👉 **Example:**

* `www.example.com`

---

# 🔹 DNS Structure (Hierarchy)

👉 Structure:

* Root (.)
* TLD (.com)
* SLD (example)
* Host (www)

---

# 🔹 TLD

👉 **Full Form:**
Top-Level Domain

👉 **Definition:**
Last part of domain name.

👉 **Examples:**

* .com
* .org
* .pk

---

# 🔹 SLD

👉 **Full Form:**
Second-Level Domain

👉 **Definition:**
Name before TLD.

👉 **Example:**

* example.com → "example" is SLD

---

# 🔹 DNS Record Types (Interview)

### 1. A Record

* Domain → IPv4
* Example: `example.com → 192.168.1.1`

---

### 2. AAAA Record

* Domain → IPv6

---

### 3. CNAME

👉 **Full Form:** Canonical Name

* Alias of another domain
* Example: `www → example.com`

---

### 4. MX

👉 **Full Form:** Mail Exchange

* Mail server record

---

### 5. TXT

* Stores text (verification, SPF, etc.)

---

### 6. NS

👉 **Full Form:** Name Server

* Defines DNS servers

---

### 7. PTR

* Reverse lookup (IP → Domain)

---

# 🔹 Azure DNS Types

### 1. Azure DNS (Public)

* Public domain hosting
* Internet accessible

---

### 2. Azure Private DNS

* Used inside VNet
* Not public

---

### 3. Custom DNS

* Your own DNS server

---

# 🔹 VNet Peering

👉 **Definition:**
Connecting two virtual networks privately.

👉 **Key Points:**

* No internet required
* Fast communication
* Secure

---

# 🔹 Auto Registration (DNS)

👉 **Definition:**
Automatically registers VM name in DNS.

👉 **Example:**

* VM1 → `vm1.internal.local`

---

# 🔹 Outbound Rule (VM → Internet)

👉 To allow VM internet access:

* Use **Network Rule** OR **Application Rule**

👉 Example:

* Allow `www.google.com`

---

