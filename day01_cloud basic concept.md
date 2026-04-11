# ☁️ 1. Azure Certification Path (Simple Roadmap)

## 🔰 Beginner (Fundamental)

**AZ-900 (Azure Fundamentals)**
Basic cloud concepts. This is the starting point for beginners.

---

## 🧑‍💻 Associate Level

* **AZ-104** → Azure Administrator
* **AZ-204** → Azure Developer
* **AZ-500** → Azure Security Engineer
* **AZ-700** → Azure Network Engineer

---

## 🧠 Expert Level

* **AZ-400** → DevOps Engineer
* **AZ-305** → Solutions Architect

---

## 📝 Exam Pattern

* MCQs: **40–65 questions**
* Total Marks: **1000**
* Passing Marks: **700**
* Cost: **~$165 USD**

---

# ☁️ 2. Cloud Fundamentals

## ❓ What is Cloud Computing?

Cloud computing is the delivery of IT resources such as servers, storage, networking, and databases over the internet on a pay-as-you-go basis instead of owning physical infrastructure.

Example: Instead of buying a server, you can create a virtual machine in Azure within minutes.

---

# ☁️ 3. Service Models (IaaS, PaaS, SaaS)

## ❓ What is IaaS?

IaaS (Infrastructure as a Service) provides virtualized infrastructure. The cloud provider manages hardware, while the user manages the operating system, applications, and data.

Example: Azure Virtual Machines

---

## ❓ What is PaaS?

PaaS (Platform as a Service) provides a platform to deploy applications without managing the underlying infrastructure or operating system.

Example: Azure App Service

---

## ❓ What is SaaS?

SaaS (Software as a Service) provides fully managed software that users can access through a web browser.

Example: Gmail, Microsoft 365

---

# ☁️ 4. Cloud Deployment Models

## ❓ What is Public Cloud?

A public cloud is a cloud environment where services are provided by a third-party provider over the internet and shared among multiple users.

Key point: It uses a multi-tenant architecture.

---

## ❓ What is Private Cloud?

A private cloud is dedicated to a single organization and provides more control, security, and customization.

---

## ❓ Difference between Private Cloud and On-Premises

On-premises infrastructure is fully hosted and managed within the organization’s physical location.
A private cloud can be hosted internally or externally but provides cloud features like scalability and automation.

---

## ❓ What is Hybrid Cloud?

Hybrid cloud is a combination of public and private cloud environments, allowing data and applications to move between them.

Example: Sensitive data in private cloud and applications in public cloud.

---

## ❓ What is Multi-Cloud?

Multi-cloud means using services from multiple cloud providers to avoid dependency on a single provider.

Example: Using Azure and AWS together.

---

# 🖥️ 5. On-Premises Infrastructure

## ❓ What is CAPEX?

CAPEX (Capital Expenditure) is the upfront cost required to purchase physical infrastructure such as servers, storage, and networking equipment.

---

## ❓ Issues in On-Premises Infrastructure

* Limited scalability
* Requires hardware maintenance
* Needs lifecycle management (replacement of hardware)
* Requires capacity planning in advance

---

# 🖥️ 6. Virtualization

## ❓ What is Virtualization?

Virtualization is the technology that allows multiple operating systems to run on a single physical machine at the same time.

---

## ❓ What is a Hypervisor?

A hypervisor is software that creates and manages virtual machines by allocating system resources such as CPU, memory, and storage.

---

## ❓ Types of Hypervisor

### Type 1 (Bare Metal)

Installed directly on physical hardware. It is more efficient and commonly used in datacenters.

Examples: Hyper-V, VMware ESXi, KVM

---

### Type 2

Runs on top of an operating system and is mainly used for testing or personal use.

Examples: VirtualBox, VMware Workstation

---

## ❓ What is a Guest OS?

A guest operating system is the operating system installed inside a virtual machine.

---

# ☁️ 7. Cloud Infrastructure

## ❓ What is Cloud Infrastructure?

Cloud infrastructure is a collection of globally distributed datacenters that provide computing, storage, networking, and other services.

---

## ❓ What does “Interconnected Datacenters” mean?

It means that datacenters are connected through high-speed private networks, allowing data transfer, replication, and failover between them.

---

## ❓ What does “Independent Datacenter” mean?

Each datacenter operates independently with its own power, cooling, and networking systems. If one datacenter fails, others continue to operate.

---

## ❓ How many datacenters are in one region?

A region contains multiple datacenters, usually grouped into Availability Zones.

---

# ☁️ 8. Azure Infrastructure

## ❓ What is a Region?

A region is a geographical area that contains multiple datacenters.

---

## ❓ What is an Availability Zone?

An Availability Zone is a physically separate datacenter within a region, designed to provide high availability and fault tolerance.

---

# ☁️ 9. Benefits of Cloud

## ❓ What is Scalability?

Scalability is the ability to increase or decrease resources based on demand.

---

### Types of Scalability

**Vertical Scaling:** Increasing CPU, RAM, or storage of a single machine.

**Horizontal Scaling:** Adding or removing multiple machines.

---

## ❓ Difference between HPA and VPA

HPA (Horizontal Pod Autoscaler) increases or decreases the number of pods.
VPA (Vertical Pod Autoscaler) increases or decreases CPU and memory of existing pods.

---

## ❓ What does “Stop Guessing Capacity” mean?

It means there is no need to predict future resource usage because cloud systems can automatically scale resources based on demand.

---

## ❓ What is Speed and Agility?

Cloud allows resources to be deployed quickly within minutes instead of waiting weeks or months.

---

## ❓ What is Redundancy?

Redundancy means having duplicate systems to ensure availability in case of failure. It includes backup, failover, and high availability.

---

# ☁️ 10. AAS (Shared Responsibility Model)

Cloud follows a shared responsibility model where deployment, maintenance, and security responsibilities are divided between the cloud provider and the user.

---

## ❓ What is IaaS? (Final Example Answer)

IaaS is a cloud service model that provides virtualized infrastructure over the internet. The cloud provider manages hardware, while the user manages the operating system and applications.
Example: Azure Virtual Machines.

