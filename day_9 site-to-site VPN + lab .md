

# 🔹 1. Site-to-Site VPN (S2S VPN)

**Definition:**
Azure VNet ↔ On-prem network **secure connection over internet (IPsec tunnel)**

👉 Means: your office network directly connected to Azure like same LAN

---

## ✅ Use Cases

* Hybrid cloud (company infra + Azure)
* Secure data transfer
* Migration from on-prem to cloud

---

# 🔹 2. Gateway Subnet

**Definition:**
Special subnet in VNet **reserved for VPN Gateway**

👉 Name MUST be:

```
GatewaySubnet
```

---

## ✅ Important Points

* No VM inside this subnet
* Only used by Azure VPN Gateway
* Recommended size: **/27 or /28**

---

# 🔹 3. VPN Gateway

**Definition:**
Azure side device that creates VPN tunnel

👉 Works like:

* Router
* VPN device

---

## ✔ Types

* Route-based (recommended)
* Policy-based (old)

---

# 🔹 4. Local Network Gateway

**Definition:**
Represents your **on-prem network in Azure**

---

## ✔ It contains:

* On-prem public IP
* On-prem address space

👉 Azure ko batata:
“mera office network yeh hai”

---

# 🔥 Architecture (Simple)

```
On-Prem Router  <==== VPN Tunnel ====>  Azure VPN Gateway
       |                                      |
 Local Network                          VNet (Azure)
```

---

# 🔥🔥🔥 LAB 3 (Full Practical)

---

# 🧪 STEP 1: Create Resource Group

1. Azure Portal → Resource Groups
2. Click **Create**
3. Name: `rg-vpn-lab`
4. Region: any (same everywhere)

---

# 🧪 STEP 2: Create VNet

1. Go → Virtual Networks → Create
2. Name: `vnet-vpn`
3. Address space:

```
10.0.0.0/16
```

---

## 🔹 Add Subnets

### ✔ Default subnet

```
Name: default
Range: 10.0.1.0/24
```

### ✔ GatewaySubnet (IMPORTANT)

```
Name: GatewaySubnet
Range: 10.0.255.0/27
```

👉 MUST exact name: GatewaySubnet

---

# 🧪 STEP 3: Create VPN Gateway

1. Search → Virtual Network Gateway
2. Click Create

---

## Fill:

* Name: `vpn-gateway`
* Region: same as VNet
* Gateway type: VPN
* VPN type: Route-based
* SKU: VpnGw1 (basic lab)

---

## Public IP:

* Create new → `vpn-gw-ip`

---

👉 Click Create (takes 30–45 mins ⏳)

---

# 🧪 STEP 4: Create Local Network Gateway

1. Go → Local Network Gateway → Create

---

## Fill:

* Name: `local-gw`
* IP address: **Your on-prem router public IP**
  (for lab: use your system/public IP)
* Address space:

```
192.168.1.0/24
```

👉 This is your local network

---

# 🧪 STEP 5: Create Connection

1. Go → VPN Gateway
2. Click **Connections → Add**

---

## Fill:

* Name: `s2s-connection`
* Connection type: Site-to-site
* Local network gateway: `local-gw`
* Shared key (PSK):

```
abc123
```

👉 Save

---

# 🧪 STEP 6: On-Prem Configuration (IMPORTANT)

👉 Real world:

* Configure router (Cisco/Mikrotik/etc)

---

## For LAB (simulation)

You can use:

* Linux VM as on-prem router

---

### Example (StrongSwan config):

Install:

```bash id="vpn1"
sudo apt update
sudo apt install strongswan -y
```

---

### Config file:

```bash id="vpn2"
sudo nano /etc/ipsec.conf
```

Add:

```
conn azure
    keyexchange=ikev2
    auto=start
    authby=psk
    left=%defaultroute
    leftid=YOUR_PUBLIC_IP
    right=AZURE_VPN_IP
    rightsubnet=10.0.0.0/16
    leftsubnet=192.168.1.0/24
```

---

### Secret key:

```bash id="vpn3"
sudo nano /etc/ipsec.secrets
```

```
YOUR_PUBLIC_IP AZURE_VPN_IP : PSK "abc123"
```

---

### Start VPN:

```bash id="vpn4"
sudo systemctl restart strongswan
```

---

# 🧪 STEP 7: Create Azure VM

1. Go → Virtual Machine → Create
2. Name: `vm-test`
3. Subnet: default

---

# 🧪 STEP 8: Test Connectivity

---

## ✔ From On-Prem → Azure

```bash id="vpn5"
ping 10.0.1.4
```

---

## ✔ From Azure → On-Prem

SSH into Azure VM:

```bash id="vpn6"
ping 192.168.1.10
```

---

# 🔍 Troubleshooting

If not working:

* Check NSG (allow ICMP)
* Check routes
* Check PSK key
* Check IP mismatch

---

# 🔥 Final Summary

| Component             | Role                                |
| --------------------- | ----------------------------------- |
| GatewaySubnet         | VPN gateway ke liye reserved subnet |
| VPN Gateway           | Azure side VPN device               |
| Local Network Gateway | On-prem representation              |
| S2S VPN               | secure tunnel                       |

---

# ⚡ Real Interview Tip

👉 Common mistake:

* Wrong GatewaySubnet name ❌
* Wrong PSK ❌
* Address space overlap ❌

