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
