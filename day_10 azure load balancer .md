# 🔥 Azure Load Balancing Services (Overview)

---

## 🔹 1. Azure Load Balancer (Layer 4 – L3/L4)

**Definition:**
Works at **transport/network layer (TCP/UDP, IP)**
👉 It does **NOT look inside HTTP/HTTPS content**

---

## ✅ Use Cases

* Simple traffic distribution
* High performance apps
* TCP/UDP apps (RDP, SSH, databases)

---

## ✔ Features

* Ultra fast
* Low latency
* No SSL termination

---

## ❌ Limitations

* No URL-based routing
* No cookie/session awareness

---

# 🔹 2. Application Gateway (Layer 7 LB)

**Definition:**
Works at **Application Layer (HTTP/HTTPS)**

---

## ✅ Use Cases

* Web apps
* URL routing (`/api` → backend1)
* SSL termination

---

## ✔ Features

* Path-based routing
* SSL offload
* Web Application Firewall (WAF)

---

## ❌ Limitations

* More expensive than L4 LB
* Slightly slower

---

# 🔹 3. Traffic Manager (DNS-Based LB)

**Definition:**
DNS level traffic routing (global)

👉 It does NOT sit in data path

---

## ✅ Use Cases

* Multi-region apps
* Disaster recovery

---

## ✔ Routing Methods

* Priority (failover)
* Performance (nearest region)
* Round-robin

---

## ❌ Limitation

* DNS caching delay

---

# 🔹 4. Front Door (Global Layer 7 LB)

**Definition:**
Global HTTP/HTTPS load balancer

---

## ✅ Use Cases

* Global apps
* CDN + caching
* Fast worldwide delivery

---

## ✔ Features

* Anycast network
* SSL
* WAF
* Global routing

---

## ❌ Limitation

* Only HTTP/HTTPS

---

# 🔥 Public vs Internal Load Balancer

---

## 🔹 Public Load Balancer

👉 Internet-facing

### Use:

* Websites
* Public APIs

---

## 🔹 Internal Load Balancer

👉 Private network only

### Use:

* Backend services
* Database tier

---

# 🔥 Quick Comparison Table

| Service         | Layer | Scope    | Use          |
| --------------- | ----- | -------- | ------------ |
| Azure LB        | L4    | Regional | TCP/UDP apps |
| App Gateway     | L7    | Regional | Web apps     |
| Traffic Manager | DNS   | Global   | Multi-region |
| Front Door      | L7    | Global   | Global web   |

---

# 🔥🔥🔥 LAB (External Load Balancer)

---

# 🧪 STEP 1: Create VNet

1. Azure Portal → Virtual Networks
2. Click **Create**

---

### Fill:

* Name: `vnet-lb`
* Address space:

```
10.1.0.0/16
```

---

### Subnet:

```
default → 10.1.1.0/24
```

---

# 🧪 STEP 2: Create Availability Set

1. Search → Availability Sets
2. Click Create

---

### Fill:

* Name: `avset-lab`
* Fault domains: 2
* Update domains: 5

---

# 🧪 STEP 3: Create VM1

1. Go → Virtual Machines → Create

---

### Fill:

* Name: `vm1`
* Image: Ubuntu
* Availability option → **Availability Set**
* Select: `avset-lab`
* VNet: `vnet-lb`

---

# 🧪 STEP 4: Create VM2

Same steps:

* Name: `vm2`
* Same availability set
* Same VNet

---

# 🧪 STEP 5: Install Nginx + Create HTML

SSH into **vm1**

```bash
sudo apt update
sudo apt install nginx -y
echo "Hello from VM1" | sudo tee /var/www/html/index.html
```

---

SSH into **vm2**

```bash
sudo apt update
sudo apt install nginx -y
echo "Hello from VM2" | sudo tee /var/www/html/index.html
```

---

# 🧪 STEP 6: Create Public Load Balancer

1. Search → Load Balancer → Create

---

### Fill:

* Name: `lb-public`
* Type: Public
* SKU: Standard

---

### Frontend IP:

* Create new Public IP

---

# 🧪 STEP 7: Backend Pool

1. Go → LB → Backend pools → Add
2. Add:

   * VM1
   * VM2

---

# 🧪 STEP 8: Health Probe

1. Go → Health probes → Add

---

### Fill:

* Protocol: HTTP
* Port: 80
* Path: `/`

---

# 🧪 STEP 9: Load Balancing Rule

1. Go → Load balancing rules → Add

---

### Fill:

* Frontend port: 80
* Backend port: 80
* Backend pool: select pool
* Probe: select probe

---

# 🧪 STEP 10: Test Load Balancer

1. Copy Public IP of LB
2. Open browser multiple times

---

## ✅ Output:

👉 Sometimes:

```
Hello from VM1
```

👉 Sometimes:

```
Hello from VM2
```

✔ That means traffic is distributed 🎯

---

# 🔥 Extra Testing (CLI loop)

```bash
while true; do curl http://LB-IP; sleep 1; done
```

---

# ⚠️ Common Issues

* NSG blocking port 80
* Nginx not running
* Probe failing

---

# 🔥 Final Understanding

* Azure LB = Fast L4 traffic distribution
* App Gateway = Smart HTTP routing
* Traffic Manager = DNS routing
* Front Door = Global web acceleration

---

