## 🌐 What is a **VPN Gateway**?

![Image](https://learn.microsoft.com/en-us/azure/vpn-gateway/media/design/multi-site.png)

![Image](https://docs.aws.amazon.com/images/whitepapers/latest/aws-vpc-connectivity-options/images/transit-gateway-and-site-to-site-vpn.png)

![Image](https://learn.microsoft.com/en-us/azure/vpn-gateway/media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

![Image](https://learn.microsoft.com/en-us/azure/vpn-gateway/media/vpn-gateway-peering-gateway-transit/gatewaytransit.png)

A **VPN Gateway** is a **managed virtual network gateway** that lets you **securely connect a Virtual Network (VNet)** to:

* On-premises networks (office/datacenter)
* Individual users (laptops/mobiles)
* Other VNets (even in different regions)

In **Microsoft Azure**, this service is called **Azure VPN Gateway**.

It uses **encrypted tunnels (IPsec/IKE)** over the public internet, so data travels safely even though the internet is used.

---

## 🎯 Why do we need a VPN Gateway? (Purpose)

Think of it like a **secure door** to your VNet.

### Main purposes:

✔ Secure connectivity over the internet
✔ Extend on-prem network to the cloud
✔ Private access to cloud resources
✔ No need for public IP exposure of VMs
✔ Cost-effective compared to dedicated circuits

---

## 🧩 How a VPN Gateway Works (Simple Flow)

```
On-Prem Network
   |
[Firewall / Router]
   |
=== Encrypted Tunnel (IPsec) ===
   |
[VPN Gateway]
   |
[Azure VNet]
   |
[VMs / Databases / Apps]
```

---

## 🏗️ How to Attach a VPN Gateway to a VNet

![Image](https://learn.microsoft.com/en-us/azure/vpn-gateway/media/vpn-gateway-peering-gateway-transit/gatewaytransit.png)

![Image](https://learn.microsoft.com/en-us/azure/vpn-gateway/media/vpn-gateway-highlyavailable/multiple-onprem-vpns.png)

![Image](https://learn-attachment.microsoft.com/api/attachments/fc16d7da-7eee-4de4-bd5d-eb9b7205c354?platform=QnA)

### Step-by-step (High level)

#### 1️⃣ Create a VNet

Example: `VNet-Prod (10.0.0.0/16)`

#### 2️⃣ Create **GatewaySubnet**

> Mandatory and **reserved only for VPN Gateway**

```
GatewaySubnet: 10.0.255.0/27
```

⚠️ No VMs or resources allowed here.

#### 3️⃣ Create VPN Gateway

* Type: **VPN**
* VPN type: **Route-based** (recommended)
* SKU: VpnGw1 / VpnGw2 / etc.
* Attach it to:

  * VNet
  * GatewaySubnet
  * Public IP

#### 4️⃣ Create Local Network Gateway (On-Prem)

Defines:

* On-prem public IP
* On-prem address space (e.g., `192.168.1.0/24`)

#### 5️⃣ Create Connection

* Type: **Site-to-Site / Point-to-Site / VNet-to-VNet**
* Shared key (pre-shared key)

---

## 🔗 Types of VPN Gateway Connections

---

### 🔹 1. Site-to-Site (S2S)

**Office ↔ Azure VNet**

![Image](https://learn.microsoft.com/en-us/azure/vpn-gateway/media/design/multi-site.png)

![Image](https://learn.microsoft.com/en-us/azure/vpn-gateway/media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

**Use case:**

* Hybrid cloud
* Servers in office accessing Azure VMs

```
Office Network ⇄ VPN Gateway ⇄ Azure VNet
```

---

### 🔹 2. Point-to-Site (P2S)

**Laptop/User ↔ Azure VNet**

![Image](https://learn.microsoft.com/en-us/azure/vpn-gateway/media/point-to-site-about/p2s.png)

![Image](https://learn.microsoft.com/en-us/azure/vpn-gateway/media/vpn-gateway-about-point-to-site-routing/branch-office.jpg)

**Use case:**

* Work from home
* Admins accessing Azure privately

```
Laptop ⇄ VPN Client ⇄ VPN Gateway ⇄ Azure VNet
```

---

### 🔹 3. VNet-to-VNet

**VNet ↔ VNet (same or different regions)**

![Image](https://learn.microsoft.com/en-us/azure/vpn-gateway/media/vpn-gateway-peering-gateway-transit/gatewaytransit.png)

![Image](https://learn.microsoft.com/en-us/azure/vpn-gateway/media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connections-diagram.png)

**Use case:**

* Multi-region architecture
* Prod ↔ DR network

```
VNet-A ⇄ VPN Gateway ⇄ VPN Gateway ⇄ VNet-B
```

---

## 🔐 Security & Encryption

VPN Gateway provides:

* **IPsec/IKE encryption**
* Authentication via:

  * Pre-shared key (S2S)
  * Certificates / Entra ID (P2S)
* Traffic stays **private inside the VNet**

---

## 🆚 VPN Gateway vs ExpressRoute (Quick Compare)

| Feature  | VPN Gateway          | ExpressRoute     |
| -------- | -------------------- | ---------------- |
| Internet | Uses public internet | Private circuit  |
| Cost     | Low                  | High             |
| Setup    | Easy                 | Complex          |
| Speed    | Up to ~1.25 Gbps     | Up to 100 Gbps   |
| Use case | Most workloads       | Mission-critical |

---

## 🧠 Real-World Example

🏢 Company has:

* Office network: `192.168.10.0/24`
* Azure VNet: `10.0.0.0/16`

They want:
✔ Azure VM to access on-prem DB
✔ Employees to access Azure apps securely

👉 Solution:

* Create VPN Gateway
* Configure Site-to-Site VPN
* Optional Point-to-Site for users

---

## ✅ Summary

✔ VPN Gateway = **secure bridge to your VNet**
✔ Must be deployed in **GatewaySubnet**
✔ Enables **hybrid & private connectivity**
✔ Supports **S2S, P2S, VNet-to-VNet**
✔ Encrypted, reliable, widely used

