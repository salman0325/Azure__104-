
### ✅ What is a VPN?

A **VPN (Virtual Private Network)** creates a **secure encrypted tunnel** over the internet between two networks or a user and a network.

👉 Think: *private connection over public internet*

---

### ✅ Why use a VPN?

* Secure communication (encryption)
* Connect remote users to cloud
* Connect two networks (on-prem ↔ cloud or cloud ↔ cloud)
* Hide internal IP structure

---

### ✅ What is a VPN Gateway in Azure?

An **Azure VPN Gateway** is a managed service that:

* Sends/receives encrypted traffic
* Enables:

  * VNet-to-VNet
  * Site-to-Site
  * Point-to-Site

---

### ✅ What is IPsec / IKE?

* **IPsec (Internet Protocol Security)** → encrypts data
* **IKE (Internet Key Exchange)** → negotiates keys and connection

👉 Together they secure VPN tunnels.

---

# 🌐 Types of Azure Connections

### 1. VNet-to-VNet

* Connect **two Azure VNets**
* Uses VPN Gateway

### 2. Site-to-Site (S2S)

* Connect **on-premises network ↔ Azure**

### 3. Point-to-Site (P2S)

* Connect **individual laptop/client ↔ Azure VNet**

### 4. ExpressRoute

* Private dedicated connection (no internet)

---

# ⚔️ VNet Peering vs VNet-to-VNet

| Feature        | VNet Peering              | VNet-to-VNet |
| -------------- | ------------------------- | ------------ |
| Speed          | Fast (Microsoft backbone) | Slower       |
| Encryption     | No                        | Yes          |
| Gateway needed | No                        | Yes          |
| Cost           | Lower                     | Higher       |

👉 Use **Peering** for same-region or trusted networks
👉 Use **VPN** when encryption required

---

# 🧪 LAB 1: VNet-to-VNet Connection (Step-by-Step)

## 🎯 Goal:

Connect two VNets in different regions and test with Ubuntu VMs

---

## 🔹 Step 1: Create VNet 1

* Name: `vnet-1`
* Region: East US (example)
* Address space: `10.1.0.0/16`

### Subnets:

* `default` → `10.1.1.0/24`
* `GatewaySubnet` → `10.1.255.0/27` ⚠️ (must be named exactly this)

---

## 🔹 Step 2: Create VNet 2

* Name: `vnet-2`
* Region: West US
* Address space: `10.2.0.0/16`

### Subnets:

* `default` → `10.2.1.0/24`
* `GatewaySubnet` → `10.2.255.0/27`

---

## 🔹 Step 3: Create VPN Gateway for VNet 1

Go to:
👉 Virtual Network Gateway → Create

Settings:

* Name: `vng-1`
* Region: same as VNet1
* Gateway type: VPN
* VPN type: Route-based
* SKU: VpnGw1 / Generation2
* Virtual network: `vnet-1`
* Public IP: `gw-public-ip-1`

⏳ Wait ~30–45 minutes

---

## 🔹 Step 4: Create VPN Gateway for VNet 2

Same steps:

* Name: `vng-2`
* Region: VNet2 region
* Public IP: `gw-public-ip-2`

---

## 🔹 Step 5: Create Connection (VNet1 → VNet2)

Go to:
👉 `vng-1` → Connections → Add

Settings:

* Connection type: VNet-to-VNet
* Gateway: `vng-1`
* Second gateway: `vng-2`
* Shared key: `12345` (same on both sides)

---

## 🔹 Step 6: Create Reverse Connection

👉 `vng-2` → Connections → Add
Repeat same (reverse direction)

---

## 🔹 Step 7: Create Ubuntu VMs

In both VNets:

* Image: Ubuntu Server 22.04
* VM1 in `vnet-1`
* VM2 in `vnet-2`

Allow:

* SSH (port 22)

---

## 🔹 Step 8: Test Connection

SSH into VM1:

```bash
ping 10.2.1.4
```

👉 If successful → VPN working ✅

---

# 🧪 LAB 2: Point-to-Site VPN (Laptop → Azure)

## 🎯 Goal:

Connect your laptop to Azure VNet using VPN

---

## 🔹 Step 1: Create VNet

* Name: `vnet-p2s`
* Address: `10.3.0.0/16`

Subnets:

* `default` → `10.3.1.0/24`
* `GatewaySubnet` → `10.3.255.0/27`

---

## 🔹 Step 2: Create VPN Gateway

* Name: `vng-p2s`
* SKU: VpnGw1
* Same settings as before

---

## 🔹 Step 3: Configure Point-to-Site

Go to:
👉 `vng-p2s` → Point-to-site configuration

Settings:

* Address pool: `172.16.0.0/24`
* Tunnel type: OpenVPN / IKEv2
* Authentication: Azure Certificate

---

## 🔹 Step 4: Create Certificates (on laptop)

### Root Certificate:

```bash
openssl req -x509 -newkey rsa:2048 -keyout root.key -out root.cer -days 365 -nodes
```

### Client Certificate:

```bash
openssl req -newkey rsa:2048 -keyout client.key -out client.csr -nodes
openssl x509 -req -in client.csr -CA root.cer -CAkey root.key -CAcreateserial -out client.cer -days 365
```

---

## 🔹 Step 5: Upload Root Certificate

* Go to Azure portal
* Upload `root.cer`

---

## 🔹 Step 6: Download VPN Client

* Click: **Download VPN client**
* Install on your laptop

---

## 🔹 Step 7: Install Client Certificate

* Install `client.cer` on your laptop

---

## 🔹 Step 8: Connect VPN

* Open VPN client
* Click Connect

---

## 🔹 Step 9: Test

SSH into VM inside VNet:

```bash
ping 10.3.1.4
```

👉 If reachable → success ✅

---

# 🔥 Important Tips

* `GatewaySubnet` name MUST be exact
* VPN Gateway takes **30–45 mins**
* Shared key must match on both sides
* NSG should allow traffic

---

