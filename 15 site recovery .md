# Azure Site Recovery (ASR) — Complete Guide

## What is Microsoft Azure Site Recovery?

Microsoft Azure Site Recovery (ASR) is a Disaster Recovery (DR) service used to:

* Replicate workloads
* Protect VMs during disasters
* Fail over applications to another region/site

It helps during:

* Datacenter failure
* Region outage
* Hardware crash
* Cyberattack
* Flood/fire disaster

---

# Main Purpose of ASR

## Backup vs Site Recovery

| Azure Backup           | Azure Site Recovery      |
| ---------------------- | ------------------------ |
| Protects data          | Protects entire workload |
| Restore files/VMs      | Keeps business running   |
| Point-in-time recovery | Automatic failover       |
| Backup copies          | Live replication         |

---

# Real World Example

```text id="glf4q4"
Primary datacenter in Karachi fails
→ ASR starts VM in Dubai region
→ Business continues running
```

---

# How Azure Site Recovery Works

![Image](https://images.openai.com/static-rsc-4/Jv7EYa_SFa_J6GCEbdA0WBqukWsG2PNevAMCB-4jmafPflFx0Bk5QhdcQDnPZzUQt6lGSoeuqsHdQE3WcDM8vab_55ZJXaI62R6fBioDVPa2mrtB2WeZ0G1yWpWOYX_uKPTq4bBEB6OYbwKWQsLXKpdgLNVPQc-USGumtT59nFmZ_fOekrYRWY_Pk0hvNzOx?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/Z38N63GDM6t6_eLaCvabLOlcknG0OYehCNPA1i8ziYWRmaDmY0Ke6R6R7OtRjOaRmxu1YA3-XnbuqBrQoHoALmljPBaIEVWNbAmazQLjfQjqwlu3LX3RCESUbKGQ0bWtdgJVIb8DNaNSSEmpcg7dqUOnVyqSjUDVQ0UZ2Y_tILByO8nVdGsFRN7IpGlkva6q?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/iMmnteSMuHB3BCDZORMqXW_nYLcWPjYIjeUXU08zYjO752o8HM1D7-bp3sjID_HUVLKzeowCm7Jqwumd42KNpQfnMdCVzvMttUZueM-wIYcTYX1dRT9aKbUz2m3VD_nomMKkzPyOL9IdEsyGRncjnctG7Q2g3j6iYNrZGg2OxcqYieEG9RJCUJ_emHQbCCOb?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/d03dwhZ844O4OTr52_2M6LfQq_yvcglOTGYQyacKXgMSLWt1yxT8Q6BmYPPsWkri_tvZjgyWtZZYk2a7qCfOp0DW1StW1y8lsPpdp41eSE0K0L5UHfYESSqEX8w_yDFFgu9HE2lYgJqsBpPceGMpiyk69XQbsUBIplQIpRmLimRzKOdMz1BB7hRgC8xGAgtN?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/qc1GULXUrZMhiexKL5NXZJT-ljO7Y3voTrfRM9p9TRchpNIhmOdgZfgWQ5HiNgJaZeTW3LS2ao1hVff83d3fBSKQ3rKDRHemmlrxMBT-hyC553i3sc0XTIZzMyeNXG56hJE364HbvdkDf7uFyP9F1LtcCC3MPQuJIAwoMS9a1axeKqI-VYEooVWHD0s0namX?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/FT2XItk1mDf3qA5iLcNPkqIv8bvtNuNwNXHaNMp8OTDEQIEoSZSDd1CRpEL_0YC8uYQ-RjfjxrWVqHk8c3Z9uKI1e-tOfs2jpt87OJ7PwUq2TJ6TYWZyDy1U3eRgUP1U9RAVbHfiZ8N3x5NhKa1kNhxcye0dPSnUjUCEx7XxZ-Bk9WH7wMyqzwKf66ddcw1T?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/Y0FRT4FrM77R3bSSRxU0CORmxohjNT20kBnYvkthc61TvMcvywslUqI6jpuRO2YQ0MlcAVapI1KBQZa-RHPTC31IkhlST0j6vCel_mWTwxYkTP5BHQy2q3aFWtp-uObA0VKXlUvAVHwYSjL1_6sKIpyXwBzRgTKkdcMwdYOG8pVaADOOcQOl3v74jsXFUqgz?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/7a36tdgrlgkAdVQiR6lXKX6KT_BPVs6F9RGWe9qBog_7WcNTX4GQMVbfzUbt-KOjswuTfRUtA5_RcbuBMdhjJfBIxiFVQRfluSmD8NvSfgFYxq7wZRlhK43qicOtYi-ArO5St0Dp0onx_AXWuNmLwV0JUnQg8sU3-f1eCzJ6X8R-HNc16gpiu4v9SsscxyLj?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/tOl4um38pe7sFP5fcK2TgJvRomSAua0zVURRINd_36w-frjUDYdYCMfO_AID1hOm0hn1RTW9N1hO4ukzRMcPrAYRAxdKqbBx8oCPnM9ctZ_6KaSNqEvlvgdI7PvyXpbN8z7gK3hKOokmEBM_atb2x8nGwSwF_9sprTX9eHUveAS-8XoFczF4cHMwUDqOH7i4?purpose=fullsize)

Flow:

```text id="n6h8wk"
Production VM
      ↓
Replication
      ↓
Recovery Services Vault
      ↓
Secondary Region
      ↓
Failover
```

---

# Core Components of ASR

| Component               | Purpose                       |
| ----------------------- | ----------------------------- |
| Recovery Services Vault | Stores replication metadata   |
| Replication Policy      | Controls replication settings |
| Failover                | Switch to DR site             |
| Failback                | Return to original site       |
| Recovery Plan           | Automated DR workflow         |

---

# ASR Supported Workloads

## Azure to Azure

* Azure VM → another Azure region

## VMware to Azure

* On-prem VMware → Azure

## Hyper-V to Azure

* Hyper-V → Azure

## Physical Servers to Azure

* Physical machines replicated

---

# Important ASR Concepts

# 1. Replication

Continuous copying of VM data to secondary site.

Example:

```text id="1q9m7f"
VM disk changes copied every few seconds
```

---

# 2. Failover

Starts VM in secondary region during disaster.

Types:

* Test Failover
* Planned Failover
* Unplanned Failover

---

# 3. Failback

Moves workload back to primary site.

---

# 4. Recovery Point

Point from which VM can be restored.

---

# 5. Recovery Plan

Automates:

* VM startup order
* Scripts
* Dependencies

Example:

```text id="5t0ow4"
Database VM starts first
Then application VM
Then web VM
```

---

# Types of Failover

## 1. Test Failover

Purpose:

* DR testing without affecting production

Creates isolated test VM.

---

## 2. Planned Failover

Used during:

* Maintenance
* Migration

Production shutdown happens properly.

---

## 3. Unplanned Failover

Used during:

* Sudden outage/disaster

Fast emergency recovery.

---

# ASR Architecture

## Azure to Azure Replication

![Image](https://images.openai.com/static-rsc-4/rn7BAWNyL6AaBboDKYV36PXqJYPbMsNwgzT2L8uYoDmVQaRiXsAxV3IIoAjY7wc-1R_KyY_gWq6SULJBITseQzQZoP0tmZsRefPk4Fj-M2_Z9hC8mLrHvNDgGTghP0idYHAdmlVRGB3mZmiEJbSek5LoXhg_zmlXXAUyzjknqLNw6g75u4x1QnpVKiZF-UI9?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/zg7BDSs9rkEamQuz9uuISO1PI7D598CsvoTuFjR2ua6UWkF5gYmEINvpKHwmZyQuTiQOFRcxht5onbW0QluDfmLqtabWI54npQ-rSCCV-m7lDuKITox22ASBwYu3-C3vuX67N0g44ratSzcJiBWMEfMkKy2Ydv0KnUh35mvFIidAw7wHMhJ_zt0pMUj-AXTt?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/S8OCVHHi-IJBaUGp-0WmaYFBpMo-Po9oPa6FwReBDN_DOuqzMZra5V5V-UxK501yHEvngJH2oiRGZcxG0PhwHkncrb_bq7pi5r9-k5qfMvpbuskokHBYxL7lCHGmtvy-eNssSxDzd-5TTeJZPeZzQilLMJ4lB_qtcZzitv2xv6Sfe_UWUIHD5EBFkemraoB-?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/l4Cg1Jl3oGI_sHVbEv_reKs4iDiTu0Qilj8B7LsS8vZhTx-lKKuLa88qYnsOLm-14phkDUmrk7WXhvJC9JYiz-VCDEXckPWAaVaNs6LkHO7dJDPMciy4H9eAkSNR65oEnneeEqpGENwKE1FLVFa3iOZEDaWQvA_PXWPp4XJyZ2zU7lIm7Q354LtZ0xORxlZ6?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/Y3nBb5U2XMrUJR659yiaTP2xjWI1NDoFC7RmZwoYRK08LyjFMDPJxfOuOOQ4Ux43bsZEFuSWGHBYP2-x68aXSY8AxXmcsfeCicovzkX2LSEb297ua2Bg-kvy-7gRMH-KFZvGSLHJDptcAc4jFlmiYv-uG977HE-ej6PMM3Uwu2dSbBBPt2TTf_hp6OMVRgPA?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/CqCxK0XZ3ih_6f_B8tKYPH80AShhVjBh0k2B7NAwiRny-Whyl-teXoe2SQhwOddyF6fSdHKdTq6s9m8azpgRWdgpCFK29R_f1F_tZYkbM1tXtfcUebj0IzXNjBBcJdrxceerm1sajK8hXBJKIaRuxCiKKh4NdBd0OTIsF_j3HyIpurfw6COqAlHYcA8SWT3f?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/e1s6BEVgLVVDtW1vKAmLmI60sKq43JqPsSZfr10uoRC40-1wnTGM7gXxxiWwH9L814Xd5pKDc-2MbUTg0UXYX0tC5N-RvP7lTVHhbc94rEY4PFBoNxOaA9sSWL7Eii8LHU0zzYg-2bQ26Cv_SW-Nda3dqNYFXpqelTPzbUtCwhgayS_xSxSeZyTofvIyK4d0?purpose=fullsize)

Process:

```text id="pnh5mc"
Azure VM
→ ASR agent
→ Recovery Services Vault
→ Secondary Region Storage
→ Failover VM
```

---

# Replication Policy Settings

| Setting                  | Example       |
| ------------------------ | ------------- |
| Recovery Point Retention | 24 hours      |
| App-consistent snapshots | Every 4 hours |
| Replication Frequency    | Continuous    |

---

# ASR Networking

During failover:

* Target VNet required
* Subnet mapping required
* IP mapping possible

---

# ASR Security Features

## Encryption

Data encrypted:

* In transit
* At rest

---

## Role-Based Access Control (RBAC)

Controls DR permissions.

---

## Network Isolation

Test failover uses isolated network.

---

# ASR Pricing

Charges for:

* Protected instances
* Storage
* Replication traffic

---

# LAB 1 — Azure VM Disaster Recovery (Azure to Azure)

## Real Industry Use Case

```text id="rq1z1d"
E-commerce company needs DR for production VM.
If primary region fails,
website should continue in another region.
```

---

# LAB Architecture

```text id="m5m6u8"
Primary VM → East US
Secondary Region → West US
```

---

# Step 1 — Create Recovery Services Vault

Search:

```text id="jtttqr"
Recovery Services Vaults
```

Click:

```text id="v4q0im"
Create
```

Fill:

| Field          | Value               |
| -------------- | ------------------- |
| Resource Group | dr-rg               |
| Vault Name     | ecommerce-asr-vault |
| Region         | East US             |

Click:

```text id="v8kntt"
Review + Create
→ Create
```

---

# Step 2 — Open Vault

Click:

```text id="njlwm6"
Go to Resource
```

---

# Step 3 — Enable Site Recovery

Inside vault:

```text id="m01q2o"
Site Recovery
→ Enable Replication
```

---

# Step 4 — Configure Source

| Setting          | Value            |
| ---------------- | ---------------- |
| Source           | Azure            |
| Source Region    | East US          |
| Deployment Model | Resource Manager |

Click:

```text id="7t5r2v"
Next
```

---

# Step 5 — Configure Target

| Setting               | Value      |
| --------------------- | ---------- |
| Target Region         | West US    |
| Target Resource Group | dr-west-rg |
| Target VNet           | dr-vnet    |

Click:

```text id="2mrl3w"
Next
```

---

# Step 6 — Select VM

Choose:

```text id="mtz0d8"
prod-web-vm
```

---

# Step 7 — Configure Replication

Policy:

* Recovery point retention → 24 hours
* App-consistent snapshot → 4 hours

Click:

```text id="kibux0"
Enable Replication
```

Replication starts.

---

# Step 8 — Verify Replication

Go:

```text id="xtyds3"
Replicated Items
```

Status should show:

```text id="gxgkjj"
Protected
```

---

# TEST FAILOVER

# Step 1

Open:

```text id="ez5j6g"
Replicated Items
```

Select VM.

---

# Step 2

Click:

```text id="0rqvpd"
Test Failover
```

---

# Step 3

Choose:

```text id="r1u92e"
Latest recovery point
```

Network:

```text id="o4xylu"
test-vnet
```

Click:

```text id="pxhml4"
OK
```

ASR creates test VM.

---

# Step 4 — Validate VM

Check:

* VM boot
* Website working
* Application access

---

# Step 5 — Cleanup Test

Click:

```text id="y5bgqv"
Cleanup Test Failover
```

---

# UNPLANNED FAILOVER

## Real Disaster

```text id="qgpr59"
Primary region suddenly crashes.
```

---

# Step 1

Select replicated VM.

Click:

```text id="8hbv35"
Failover
```

---

# Step 2

Choose:

```text id="srb0vr"
Latest processed recovery point
```

Check:

```text id="4kmw86"
Shut down machine before failover
```

(if available)

---

# Step 3

Click:

```text id="52js91"
OK
```

ASR starts VM in DR region.

---

# Step 4 — Commit Failover

After verification:

```text id="vcj0t6"
Commit
```

Disaster recovery complete.

---

# FAILBACK

After primary region restored:

```text id="gppwfr"
Re-Protect
→ Failback
```

VM returns to original region.

---

# LAB 2 — VMware On-Premises to Azure DR

## Real Industry Use Case

```text id="6ly1mn"
Bank has VMware servers on-premises.
Needs disaster recovery to Azure.
```

---

# Architecture

![Image](https://images.openai.com/static-rsc-4/cUO4P2vdEewdg0AESVBOGMJ7VZ4TKxfxR65Fb9vpnOg2eooX_lI03NH6tyMJTM0932PG2v9RYWBPGIs188WdUoiRaPsDecjit_DBZOiLyXR4KHSRmHAyXQgvJvaMFcutdSXsatOXZivrmMVV-2UaTFgS-G35EOGjLS9gb4wnYN_JgU-ciky_3wuyt9mLBZ7y?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/GQWd0D7XY3NoowgMCUIjeSM74ES-VfckGRfoYuZq8qUNYRiyKJTrcJbdgRGNLBj4hh-6Nu86c0ynqZSiaCeMYkzU7mLAdfHic25tPeF9vCv8mq_vse2Y3fK7z1COFbh_bZEOImcMgH9jwcUViLxO-b4IOkavxyexCdIrLrWaWghAlrf5mpl6Gp6PYvvRDy0p?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/73GWRmckxZimgrOu_oBCx9Gwy2lwkaornEk-iTCrQRduIJmV88rm4t0mkD5v9POIbg-oFR4NKZleg4u6_7bfEgB6OXk8GMadJ4giUJxkSsdgCYOefvvlC-C_9sOpDxfC-RA1ykyTefqDTGGMJ82w4sQoxHmdcmZnFug5gTY5ItgWb9xqBMGVmYRJklqi7efw?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/mJvTpjSAqOxsfpFtPjs8gtok7o_0qThIqldTxlyl09EazuI6fNxQkY-e2-ZV5H36Cbkom_R39s70CES8OB-lb6dW4kcxyw3XZv_UF7sPfSrVj8kgEhOu6dNaNpMpso3GC9KNpvKQM_JubUIY2cDxMtc1lMivXhuufwgkRdp86cnceRwYFMsA-2aMDlDHFU7G?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/A_HKNY7FnUybP3P_TR9tcxGRD53TkensYQVuzrrx0Be83Bw5H4ctlqWyU5OSTpc3iAobjMkjX0qiI5uq5Tts3lsOPIADorUHP3t0n1JE6Ec8c6kdOkbYYHLVEsidfS9iXZ_laZxGbh8BtSoianoA5rta6znmkDmqiGjPs5jOgEndjRN3X6aNwDB4BMwrZ3HD?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/eNS7jj-IcBrdSxNlfssoimw34XT1Rx87xWTdTd6T-ERtH6HpwvC98L-X9r1zaHlj0-xxL8gLIcj8r6_11D6C5T-IuVViet49-eY6TOuwdQvm4dZuRlHgb11t3g_a21JhSdNGYFT8rjFrAhDB8aZU0mpkmVhG5Zz7iHw0CVJbJUKy7gdYvSBU1lTITqrLdNv2?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/D4to00g868BEcA9T5ugLcJmsFDSt9ucU0wOOGeO8czfTygk3JfRzGy7n42IvdQIQK7Gtcq0ibOtVGSEI7LMWNoFMa_ICMRbqWyC7-m_UNDmHEZosFMw8n3X2lmjIW3B-mhB4hR7OAl8lpiztrjP7sBDmOpx8OkRxkWiwig17Xyg8wv8gMZfpGePZFmdFXn_s?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/USJHRqV-tmud1NKWrdOVPkOlwAj0mtVCMu6IyoXBDiFuoW9e9IV87dECDbl_5kSJIleY2WQlgQ4GAgpXFpnqNAtofPA5Z0l3qgca9jO4bKw8hHGPB-6v_8lVK9OuMmYhTViRWYBn2r6i9BN4xxqsbHk2eqBC1IOIiOVnIck4VqSwj5RF6Yaxxoor0LDNS7YI?purpose=fullsize)

Flow:

```text id="x9k4me"
VMware VM
→ Configuration Server
→ Azure Site Recovery
→ Azure VM
```

---

# Components Required

| Component            | Purpose                  |
| -------------------- | ------------------------ |
| Configuration Server | Handles replication      |
| Process Server       | Data transfer            |
| Master Target Server | Linux replication target |

---

# Step 1 — Create Recovery Services Vault

Same process as previous lab.

---

# Step 2 — Prepare VMware Environment

Requirements:

* VMware vCenter
* Internet connectivity
* Windows Server for Configuration Server

---

# Step 3 — Download ASR Appliance

Inside vault:

```text id="s8vf1s"
Site Recovery Infrastructure
→ VMware & Physical Machines
```

Download:

* OVF template
* Registration key

---

# Step 4 — Deploy Configuration Server

Deploy OVF in VMware.

Configure:

* IP
* DNS
* Timezone

---

# Step 5 — Register Configuration Server

Open appliance portal.

Enter:

```text id="mr2twj"
Vault registration key
```

Server registers with Azure.

---

# Step 6 — Add vCenter Server

Inside appliance:

```text id="xq9yot"
Add vCenter
```

Enter:

* vCenter IP
* Username
* Password

---

# Step 7 — Enable Replication

Go Azure Portal:

```text id="22om24"
Recovery Services Vault
→ Replicate Application
```

Choose:

```text id="w3kj7z"
VMware vSphere
```

Select:

* Configuration server
* VMware VM
* Target Azure resources

---

# Step 8 — Start Replication

Click:

```text id="8p7h3l"
Enable Replication
```

---

# Step 9 — Perform Test Failover

Same as Azure VM failover:

```text id="lbygrl"
Replicated Items
→ Test Failover
```

---

# Recovery Plans

## What is Recovery Plan?

Automated DR workflow.

Example startup order:

1. Database
2. Backend API
3. Frontend servers

---

# Create Recovery Plan

Go:

```text id="ag0wz2"
Recovery Plans
→ Create Recovery Plan
```

Add VMs.

Arrange startup sequence.

---

# ASR Best Practices

| Best Practice               | Reason              |
| --------------------------- | ------------------- |
| Run regular test failovers  | Verify DR works     |
| Use separate DR network     | Avoid conflicts     |
| Protect critical apps first | Business continuity |
| Monitor replication health  | Avoid sync issues   |
| Use Recovery Plans          | Automation          |

---

# Backup vs ASR — Final Difference

| Feature | Azure Backup | Azure Site Recovery |
|---|---|
| Purpose | Data recovery | Business continuity |
| Replication | No | Yes |
| Automatic failover | No | Yes |
| DR orchestration | No | Yes |
| Recovery speed | Slower | Faster |
| Main Use | Backup/restore | Disaster recovery |

---

# Important Interview Questions

## Q1. Difference between Planned and Unplanned Failover?

| Planned              | Unplanned          |
| -------------------- | ------------------ |
| Controlled migration | Emergency disaster |
| Minimal data loss    | Possible data loss |
| Maintenance use      | Outage use         |

---

## Q2. Why use Test Failover?

Answer:

```text id="p7p1vw"
To test disaster recovery without affecting production.
```

---

# Complete ASR Workflow

```text id="ty2e9u"
Production VM
      ↓
Replication Enabled
      ↓
Data Copied to Secondary Region
      ↓
Disaster Happens
      ↓
Failover Triggered
      ↓
VM Starts in DR Region
      ↓
Business Continues
```
