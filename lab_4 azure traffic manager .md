# LAB 1 — Azure Traffic Manager (Priority / Failover)

Goal:

✅ Create 2 App Services
✅ Create Traffic Manager
✅ Configure Priority Routing
✅ Test Failover in Browser

---

# Architecture

```plaintext id="7zvf7h"
User
  |
Traffic Manager
  |
-------------------------
|                       |
Primary App         Secondary App
Priority 1          Priority 2
```

---

# STEP 1 — Create Resource Group

Go to:

```plaintext id="6f80da"
Azure Portal
```

Search:

```plaintext id="6wg5zd"
Resource Groups
```

Click:

```plaintext id="um40rk"
Create
```

Fill:

| Setting        | Value     |
| -------------- | --------- |
| Resource Group | rg-tm-lab |
| Region         | East US   |

Click:

```plaintext id="v2xjpk"
Review + Create
Create
```

---

# STEP 2 — Create First App Service

Search:

```plaintext id="6hcbqq"
App Services
```

Click:

```plaintext id="t4yv79"
Create
```

---

## Basic Tab

| Setting          | Value              |
| ---------------- | ------------------ |
| Resource Group   | rg-tm-lab          |
| Name             | tm-app-primary-123 |
| Publish          | Code               |
| Runtime Stack    | PHP 8.2            |
| Operating System | Linux              |
| Region           | East US            |
| Pricing Plan     | B1                 |

Click:

```plaintext id="kjv4lf"
Review + Create
Create
```

---

# STEP 3 — Create Second App Service

Again:

```plaintext id="b8n9ie"
App Services → Create
```

Fill:

| Setting        | Value                |
| -------------- | -------------------- |
| Resource Group | rg-tm-lab            |
| Name           | tm-app-secondary-123 |
| Runtime Stack  | PHP 8.2              |
| OS             | Linux                |
| Region         | West Europe          |
| Pricing Plan   | B1                   |

Click:

```plaintext id="59q0vl"
Review + Create
Create
```

---

# STEP 4 — Add Simple Web Page to Both Apps

Open:

```plaintext id="pjlwmj"
tm-app-primary-123
```

Go:

```plaintext id="6ttv8u"
Development Tools
→ Advanced Tools
→ Go
```

Open:

```plaintext id="jz3kcg"
Debug Console
→ CMD
→ site/wwwroot
```

Create:

```plaintext id="l6o3g6"
index.html
```

Paste:

```html
<h1>PRIMARY APP - EAST US</h1>
```

Save.

---

Do same for second app.

Content:

```html
<h1>SECONDARY APP - WEST EUROPE</h1>
```

Save.

---

# STEP 5 — Create Traffic Manager

Search:

```plaintext id="p6j8g0"
Traffic Manager Profiles
```

Click:

```plaintext id="8ucmzu"
Create
```

---

## Fill Details

| Setting        | Value             |
| -------------- | ----------------- |
| Name           | tm-priority-demo  |
| Routing Method | Priority          |
| Subscription   | Your Subscription |
| Resource Group | rg-tm-lab         |

Click:

```plaintext id="5j0qsa"
Create
```

---

# STEP 6 — Add Primary Endpoint

Open:

```plaintext id="4q3x8d"
tm-priority-demo
```

Go:

```plaintext id="aq6vpy"
Endpoints
→ Add
```

Fill:

| Setting              | Value              |
| -------------------- | ------------------ |
| Type                 | Azure Endpoint     |
| Name                 | primary-endpoint   |
| Target Resource Type | App Service        |
| Target Resource      | tm-app-primary-123 |
| Priority             | 1                  |

Click:

```plaintext id="xzx0up"
Add
```

---

# STEP 7 — Add Secondary Endpoint

Again:

```plaintext id="6i7o3v"
Endpoints → Add
```

Fill:

| Setting         | Value                |
| --------------- | -------------------- |
| Type            | Azure Endpoint       |
| Name            | secondary-endpoint   |
| Target Resource | tm-app-secondary-123 |
| Priority        | 2                    |

Click:

```plaintext id="7r06aj"
Add
```

---

# STEP 8 — Test in Browser

Open Traffic Manager.

Copy:

```plaintext id="n0md24"
DNS Name
```

Example:

```plaintext id="lxw3pw"
tm-priority-demo.trafficmanager.net
```

Open in browser.

Result:

```plaintext id="z43qhh"
PRIMARY APP - EAST US
```

Because Priority 1 active.

---

# STEP 9 — Test Failover

Go to:

```plaintext id="u6iwvc"
primary-endpoint
```

Click:

```plaintext id="k6s3m7"
Disable
```

Wait:

```plaintext id="46dr0s"
1–2 minutes
```

Refresh browser.

Now result:

```plaintext id="6gmlt6"
SECONDARY APP - WEST EUROPE
```

Failover working.

---

# LAB 1 COMPLETE ✅

---

# LAB 2 — Traffic Manager Performance Routing (Cross Region)

Goal:

✅ Create 2 VNets in different regions
✅ Create 2 VMs
✅ Install web server
✅ Configure Traffic Manager Performance Routing
✅ Users connect to nearest region automatically

---

# Architecture

```plaintext id="gm6kmr"
Pakistan User
     |
Traffic Manager
     |
-------------------------
|                       |
India VM            Europe VM
```

Nearest region responds first.

---

# STEP 1 — Create Resource Group

Search:

```plaintext id="5yxtql"
Resource Groups
```

Create:

| Setting | Value              |
| ------- | ------------------ |
| Name    | rg-performance-lab |

Create.

---

# STEP 2 — Create VNet 1 (India)

Search:

```plaintext id="r6epyd"
Virtual Networks
```

Click:

```plaintext id="r1l2wq"
Create
```

Fill:

| Setting       | Value         |
| ------------- | ------------- |
| Name          | india-vnet    |
| Region        | Central India |
| Address Space | 10.1.0.0/16   |
| Subnet        | 10.1.1.0/24   |

Create.

---

# STEP 3 — Create VNet 2 (Europe)

Again create:

| Setting       | Value       |
| ------------- | ----------- |
| Name          | europe-vnet |
| Region        | West Europe |
| Address Space | 10.2.0.0/16 |
| Subnet        | 10.2.1.0/24 |

Create.

---

# STEP 4 — Create India VM

Search:

```plaintext id="r7kgm8"
Virtual Machines
```

Click:

```plaintext id="4jl7g0"
Create
```

Fill:

| Setting  | Value          |
| -------- | -------------- |
| Name     | india-vm       |
| Region   | Central India  |
| Image    | Ubuntu 22.04   |
| Size     | B1s            |
| Username | azureuser      |
| Password | Password@12345 |

---

## Networking

| Setting         | Value      |
| --------------- | ---------- |
| Virtual Network | india-vnet |
| Public IP       | Create New |

---

## Inbound Ports

Enable:

```plaintext id="f6kk8v"
HTTP
SSH
```

Create VM.

---

# STEP 5 — Create Europe VM

Same process.

| Setting | Value       |
| ------- | ----------- |
| Name    | europe-vm   |
| Region  | West Europe |
| VNet    | europe-vnet |

Create.

---

# STEP 6 — Install Apache on India VM

Open:

```plaintext id="k1t4w8"
india-vm
→ Connect
→ SSH
```

Run:

```bash
sudo apt update
sudo apt install apache2 -y
```

---

Create page:

```bash
echo "<h1>INDIA SERVER</h1>" | sudo tee /var/www/html/index.html
```

Restart:

```bash
sudo systemctl restart apache2
```

---

# STEP 7 — Install Apache on Europe VM

SSH into Europe VM.

Run:

```bash
sudo apt update
sudo apt install apache2 -y
```

Create page:

```bash
echo "<h1>EUROPE SERVER</h1>" | sudo tee /var/www/html/index.html
```

Restart:

```bash
sudo systemctl restart apache2
```

---

# STEP 8 — Test Both VMs

Open:

```plaintext id="qj9d2g"
India VM Public IP
```

Should show:

```plaintext id="v0kwx6"
INDIA SERVER
```

---

Open Europe VM Public IP.

Should show:

```plaintext id="q9g26q"
EUROPE SERVER
```

---

# STEP 9 — Create Traffic Manager

Search:

```plaintext id="et1zwd"
Traffic Manager Profiles
```

Create.

Fill:

| Setting        | Value               |
| -------------- | ------------------- |
| Name           | tm-performance-demo |
| Routing Method | Performance         |
| Resource Group | rg-performance-lab  |

Create.

---

# STEP 10 — Add India Endpoint

Open:

```plaintext id="9h9jlwm"
Endpoints
→ Add
```

Fill:

| Setting | Value              |
| ------- | ------------------ |
| Type    | External Endpoint  |
| Name    | india-endpoint     |
| Target  | India VM Public IP |

Add.

---

# STEP 11 — Add Europe Endpoint

Again:

| Setting | Value               |
| ------- | ------------------- |
| Type    | External Endpoint   |
| Name    | europe-endpoint     |
| Target  | Europe VM Public IP |

Add.

---

# STEP 12 — Test Performance Routing

Copy Traffic Manager DNS:

Example:

```plaintext id="mbg4ya"
tm-performance-demo.trafficmanager.net
```

Open in browser.

---

# Expected Result

Since Pakistan closer to India:

You should see:

```plaintext id="hy0i7j"
INDIA SERVER
```

---

# STEP 13 — Test Automatic Switching

Stop India VM.

Go:

```plaintext id="x3c1bx"
india-vm
→ Stop
```

Wait:

```plaintext id="5jlwm1"
2 minutes
```

Refresh browser.

Now:

```plaintext id="jmm62m"
EUROPE SERVER
```

Traffic Manager automatically routed to next healthy region.

---

# LAB 2 COMPLETE ✅

---

# Important Concept

| Routing     | Behavior                |
| ----------- | ----------------------- |
| Priority    | Main + Backup           |
| Performance | Nearest Region          |
| Weighted    | Percentage Distribution |
| Geographic  | Country Based           |
| Multivalue  | Multiple Healthy IPs    |
| Subnet      | IP Range Based          |
