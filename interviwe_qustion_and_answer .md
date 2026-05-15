# 1. Difference Between NSG and ASG in Azure

## NSG (Network Security Group)

An Azure Network Security Group is used to **allow or deny network traffic**.

It works like a firewall rule for:

* Subnet level
* VM NIC (Network Interface) level

You create rules such as:

* Allow HTTP (80)
* Allow SSH (22)
* Deny all inbound traffic

### Example

Suppose:

* Web VM needs port 80 open
* Database VM should only allow SQL traffic

You create NSG rules:

* Allow TCP 80 for Web VM
* Allow TCP 1433 only from Web subnet to DB subnet

---

## ASG (Application Security Group)

An Azure Application Security Group is used to **group VMs logically**.

Instead of writing IP addresses in NSG rules, you use groups.

### Example

You have:

* 5 Web servers
* 3 Database servers

Create:

* ASG-Web
* ASG-DB

Now NSG rule becomes:

> Allow traffic from ASG-Web → ASG-DB on port 1433

No need to manage IP addresses manually.

---

## Main Difference

| NSG                 | ASG                      |
| ------------------- | ------------------------ |
| Security rules      | Logical grouping         |
| Filters traffic     | Organizes VMs            |
| Works on subnet/NIC | Used inside NSG rules    |
| Like firewall       | Like VM grouping/tagging |

---

# 2. How Can You Block Access to Your VM From a Subnet?

You can block access using an Azure Network Security Group rule.

### Example

Suppose:

* VM is in Subnet-A
* You want to block traffic coming from Subnet-B

Create NSG rule:

| Source   | Destination | Action |
| -------- | ----------- | ------ |
| Subnet-B | VM/Subnet-A | Deny   |

### Real Example

Deny:

* Source: 10.0.2.0/24
* Destination: 10.0.1.4
* Port: Any
* Action: Deny

Traffic from that subnet will be blocked.

---

# 3. Are Azure NSGs Stateful or Stateless?

Azure Network Security Group are **Stateful**.

## Meaning

If inbound traffic is allowed,
then return traffic is automatically allowed.

You do NOT need separate outbound rule for response traffic.

### Example

You allow:

* Internet → VM on port 80

User opens website.

The response traffic from VM back to user is automatically allowed.

---

# 4. Difference Between Azure Firewall and NSG

## NSG

Azure Network Security Group provides:

* Basic traffic filtering
* Layer 3 and Layer 4 security
* Allow/Deny rules
* Works on subnet or NIC

### Checks:

* IP
* Port
* Protocol

---

## Azure Firewall

Azure Firewall is a fully managed centralized firewall.

Provides:

* Advanced filtering
* Threat intelligence
* Application rules
* FQDN filtering
* DNAT/SNAT
* Logging

### Checks:

* Website/domain names
* URLs
* Applications
* Traffic patterns

---

## Easy Interview Difference

| NSG               | Azure Firewall                |
| ----------------- | ----------------------------- |
| Basic security    | Advanced centralized security |
| Subnet/NIC level  | VNet level                    |
| Layer 3/4         | Layer 3–7                     |
| Free/cheap        | More expensive                |
| Simple allow/deny | Intelligent filtering         |

---

# 5. Advantages of Resource Groups in Azure

A Azure Resource Group is a logical container for Azure resources.

## Advantages

### 1. Easy Management

Manage related resources together.

Example:

* VM
* Storage
* VNet
* Database

inside one resource group.

---

### 2. Access Control

Apply RBAC permissions on entire group.

Example:

* Dev team gets access only to Dev-RG

---

### 3. Easy Monitoring

Monitor billing, logs, and metrics together.

---

### 4. Easy Deletion

Delete whole environment at once.

Example:
Delete testing environment quickly.

---

### 5. Automation

Useful in ARM/Bicep/Terraform deployments.

---

# 6. Difference Between Azure User Data and Custom Data

## Custom Data

Azure Virtual Machines Custom Data is used to pass startup scripts/configurations during VM creation.

Mostly used with:

* cloud-init (Linux)

### Example

Install nginx automatically when VM starts.

---

## User Data

User Data is newer and more flexible.

It allows applications inside VM to access metadata/user information after VM deployment.

Can be updated/read more easily.

---

## Simple Difference

| Custom Data             | User Data                |
| ----------------------- | ------------------------ |
| Mainly startup config   | Runtime/application data |
| Used during VM creation | Can be accessed later    |
| Mostly cloud-init       | More flexible            |

---

# 7. Difference Between Azure Application Gateway and Azure Load Balancer

## Azure Load Balancer

Azure Load Balancer works at:

* Layer 4 (TCP/UDP)

It distributes traffic based on:

* IP
* Port

### Example

Distribute traffic between 3 web servers.

---

## Azure Application Gateway

Azure Application Gateway works at:

* Layer 7 (HTTP/HTTPS)

Can:

* Understand URLs
* SSL termination
* Web Application Firewall (WAF)
* Cookie-based sessions
* Path routing

### Example

* `/images` → Image server
* `/api` → API server

---

## Main Difference

| Load Balancer   | App Gateway        |
| --------------- | ------------------ |
| Layer 4         | Layer 7            |
| TCP/UDP traffic | HTTP/HTTPS traffic |
| Fast/simple     | Smart web routing  |
| No WAF          | Supports WAF       |

---

# 8. Traffic Flow to Your Application in Azure

Assume company setup:

* Internet users
* Azure Frontend
* Web subnet
* App subnet
* DB subnet
* NSGs
* Firewall
* Bastion

## Traffic Flow

### Step 1 — User Request

User opens website:

```text
https://company.com
```

---

### Step 2 — DNS Resolution

DNS resolves domain to public IP.

---

### Step 3 — Application Gateway

Traffic reaches Azure Application Gateway.

Tasks:

* SSL termination
* WAF inspection
* URL routing

---

### Step 4 — NSG Check

Azure Network Security Group checks:

* Allowed ports
* Allowed sources

Example:

* Allow HTTPS 443
* Deny unwanted traffic

---

### Step 5 — Web Subnet

Traffic reaches Web servers.

Web app processes request.

---

### Step 6 — App Subnet

Web tier communicates with backend API/app servers.

---

### Step 7 — Database Subnet

Backend accesses database securely.

Usually:

* Private IP only
* No internet access

---

### Step 8 — Response Back

Response returns to user through same path.

---

## Short Interview Answer

> User traffic comes from internet → DNS → Application Gateway/WAF → NSG filtering → Web subnet → App subnet → Database subnet. Security is controlled using NSGs, Firewall, and private subnet communication.

---

# 9. Purpose of Azure Bastion

Azure Bastion provides secure RDP/SSH access to VMs directly from Azure Portal.

## Why It Is Used

Normally:

* VM needs Public IP for RDP/SSH

This is risky.

Bastion solves this problem.

---

## How Bastion Works

Admin connects:

```text
Azure Portal → Bastion → VM
```

Connection happens securely over browser.

VM does NOT need:

* Public IP
* Open RDP port
* Open SSH port

---

## Advantages

| Feature              | Benefit                |
| -------------------- | ---------------------- |
| No Public IP         | Better security        |
| Browser-based access | Easy management        |
| Secure RDP/SSH       | Reduced attack surface |

---

## Interview Style Answer

> Azure Bastion is used for secure remote management of Azure VMs using RDP or SSH through the Azure Portal without exposing VMs to the public internet. It improves security by removing the need for public IP addresses on virtual machines.
