# What is Microsoft Azure Traffic Manager?

Think of Azure Traffic Manager like an **internet traffic police**.

When users open your website or app, Traffic Manager decides:

👉 **Which server/location should handle the request?**

It works at **DNS level** (Domain Name System).

It does NOT directly forward traffic like a load balancer.

Instead:

1. User types `myapp.com`
2. DNS asks Traffic Manager
3. Traffic Manager replies:

   * “Go to USA server”
   * OR “Go to Europe server”
   * OR “Go to backup server”

Then user connects directly to that endpoint.

---

# Real Definition

## Azure Traffic Manager

A DNS-based global traffic load balancer service in Azure that distributes user traffic across multiple application endpoints.

---

# Why Do We Need It?

Without Traffic Manager:

* If one server crashes → website down
* Users far away → slow performance
* All traffic goes to one location
* No disaster recovery

Traffic Manager solves these problems.

---

# Real Life Example

Imagine:

You have app servers in:

* USA
* Germany
* India

Now:

* USA users should go to USA server
* Indian users should go to India server
* If India server fails → redirect to Germany

Traffic Manager does this automatically.

---

# Simple Architecture

```plaintext
             Users
               |
               v
      Azure Traffic Manager
               |
   -------------------------
   |           |           |
USA Server   India       Germany
             Server       Server
```

Traffic Manager only tells user WHICH server to use.

---

# Key Features

## 1. Global Load Balancing

Distributes traffic globally.

Example:

* Asian users → Asia server
* Europe users → Europe server

---

## 2. Automatic Failover

If one endpoint/server fails:

Traffic automatically shifts to healthy endpoint.

---

## 3. High Availability

Application remains online even if:

* VM crashes
* Region fails
* Datacenter issue occurs

---

## 4. DNS-Based Routing

Works using DNS queries.

Not proxy-based.

---

## 5. Multiple Routing Methods

Supports:

* Priority
* Weighted
* Performance
* Geographic
* Multivalue
* Subnet

---

# What is an Endpoint?

Endpoint means:

👉 Destination where traffic is sent.

Example:

* VM public IP
* App Service URL
* External website
* Another Traffic Manager profile

---

# Types of Endpoints

There are 3 main endpoint types.

---

# 1. Azure Endpoint

Resources inside Azure.

Examples:

* Azure VM
* App Service
* AKS ingress
* Public Load Balancer

---

## Example

```plaintext
trafficmanager.net
        |
        v
Azure App Service
```

Example URL:

```plaintext
mywebapp.azurewebsites.net
```

---

# 2. External Endpoint

Resources OUTSIDE Azure.

Could be:

* AWS server
* On-prem server
* Physical datacenter
* External public IP

---

## Example

```plaintext
Traffic Manager
      |
      v
AWS EC2 Server
```

or

```plaintext
Traffic Manager
      |
      v
On-Prem Datacenter
```

---

# 3. Nested Endpoint

Traffic Manager inside another Traffic Manager.

Means:

* One parent profile
* Multiple child profiles

Used for very large architectures.

---

## Example

```plaintext
Global Traffic Manager
        |
 -------------------
 |                 |
Asia TM         Europe TM
 |                 |
Servers          Servers
```

---

# What is Routing Method?

Routing method decides:

👉 HOW Traffic Manager selects endpoint.

Different methods solve different business problems.

---

# 1. Priority Routing (Failover)

Also called:

✅ Failover Routing

---

## Purpose

Used for:

* Backup system
* Disaster recovery

Only ONE primary endpoint handles traffic.

If it fails:

* Traffic moves to backup endpoint.

---

## Example

```plaintext
Priority 1 → USA Server
Priority 2 → Germany Backup
Priority 3 → India Backup
```

---

## Working

Normal Condition:

```plaintext
All traffic → USA
```

USA Down:

```plaintext
All traffic → Germany
```

Germany Down:

```plaintext
All traffic → India
```

---

## Real Scenario

Banking application.

Need:

* Main production server
* DR site backup

---

# 2. Weighted Routing (Distribution)

Traffic distributed based on assigned weight.

---

## Purpose

Used for:

* Load distribution
* Testing
* Gradual rollout

---

## Example

```plaintext
USA Server     Weight 80
India Server   Weight 20
```

Meaning:

* 80% traffic → USA
* 20% traffic → India

---

## Real Scenario

New version testing.

```plaintext
Old App → 90%
New App → 10%
```

Safe deployment.

---

# 3. Performance Routing

Traffic goes to LOWEST latency endpoint.

Closest/fastest server selected.

---

## Example

User from Pakistan:

```plaintext
Pakistan User → India Server
```

User from Germany:

```plaintext
Germany User → Europe Server
```

---

## Purpose

Improve:

* Speed
* User experience
* Low latency

---

# Example

Without Performance Routing:

```plaintext
Pakistan user → USA server
```

Slow.

With Performance Routing:

```plaintext
Pakistan user → India server
```

Fast.

---

# 4. Geographic Routing

Traffic routed based on user geographic region.

---

## Purpose

Used for:

* Legal compliance
* Language-based apps
* Region restrictions

---

## Example

```plaintext
Pakistan users → Pakistan site
Europe users → Europe site
USA users → USA site
```

---

## Real Scenario

Streaming platform.

EU users must stay in EU because of GDPR laws.

---

# 5. Multivalue Routing

Returns multiple healthy endpoints.

Mainly used for:

* High availability
* Client-side retry

---

## Example

Traffic Manager returns:

```plaintext
Server1 IP
Server2 IP
Server3 IP
```

Client tries one.

If failed:

* tries another.

---

## Real Scenario

DNS-based redundancy.

---

# 6. Subnet Routing

Routes users based on source IP subnet.

---

# What is Subnet?

Subnet means IP range.

Example:

```plaintext
192.168.1.0/24
10.0.0.0/16
```

---

## Purpose

Specific networks go to specific endpoints.

---

## Example

```plaintext
Office Karachi IP range → Karachi server
Office Lahore IP range → Lahore server
```

---

# Real Corporate Example

Company has offices:

| Office  | IP Range    | Endpoint    |
| ------- | ----------- | ----------- |
| Karachi | 10.1.0.0/16 | Karachi App |
| Lahore  | 10.2.0.0/16 | Lahore App  |

Traffic Manager routes accordingly.

---

# Health Checks (Very Important)

Traffic Manager continuously checks endpoint health.

Example:

```plaintext
HTTP
HTTPS
TCP
```

If endpoint unhealthy:

* Removed automatically.

---

# Difference Between Traffic Manager and Load Balancer

| Feature        | Traffic Manager      | Load Balancer           |
| -------------- | -------------------- | ----------------------- |
| Works at       | DNS Level            | Network Level           |
| Scope          | Global               | Regional                |
| Main Purpose   | Route users globally | Balance traffic locally |
| Protocol       | DNS                  | TCP/UDP                 |
| Internet aware | Yes                  | Usually regional        |

---

# Traffic Manager vs Front Door

| Feature     | Traffic Manager | Azure Front Door  |
| ----------- | --------------- | ----------------- |
| Layer       | DNS             | Application Layer |
| Routing     | DNS-based       | HTTP/HTTPS        |
| Caching     | No              | Yes               |
| WAF         | No              | Yes               |
| SSL Offload | No              | Yes               |

---

# Simple Memory Trick

| Routing Method | Meaning              |
| -------------- | -------------------- |
| Priority       | Backup/Failover      |
| Weighted       | Percentage Traffic   |
| Performance    | Closest Server       |
| Geographic     | Country/Region Based |
| Multivalue     | Multiple Healthy IPs |
| Subnet         | IP Range Based       |

---

# Complete Real World Example

Company has:

* USA region
* Europe region
* India region

Needs:

* Fast access
* Backup
* Region control

Setup:

```plaintext
Performance Routing
```

Users automatically connect to nearest region.

Backup:

```plaintext
Priority Failover
```

If India fails:

```plaintext
India traffic → Europe
```

EU laws:

```plaintext
Geographic Routing
```

EU users remain in EU.

---

# Final One-Line Definition

## Azure Traffic Manager

A DNS-based global traffic routing service that directs users to the best available application endpoint based on routing rules and endpoint health.
