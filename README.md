# 🏢 Small Organization Network Setup – Cisco Packet Tracer

This repository contains the configuration and documentation for a **multi-subnet corporate network simulation** built in **Cisco Packet Tracer**.

---

## 🎯 Goal

To design, configure, and verify connectivity across **four distinct local area networks (LANs)** using a **central router** for inter-network communication, and to deploy basic **DNS and Web (HTTP)** services on a central server.

---

## 💻 Network Topology Overview

The network is divided into four main sections, each representing a department with its own **Layer 3 network segment**.  
A single router acts as the **gateway** for all internal traffic.

| Section / Department          | Network Address  | Default Gateway (Router Interface) | Key Devices      |
|-------------------------------|------------------|------------------------------------|------------------|
| Database / Server             | 192.168.1.0/24   | 192.168.1.1 (Fa1/0)                | 1 Server         |
| Administration                | 192.168.2.0/24   | 192.168.2.1 (Fa0/0)                | 2 PCs            |
| Accounts & Finance            | 192.168.3.0/24   | 192.168.3.1 (Fa0/1)                | 2 PCs            |
| Information Technology (IT)   | 192.168.4.0/24   | 192.168.4.1 (Fa1/1)                | 2 PCs            |

> **Note:** Router interface names may vary (e.g., `Fa4/0`, `Gig0/0/0`), depending on the model/modules used in Packet Tracer.

---

## 🛠️ Hardware & Components

| Device  | Quantity | Model (Recommended)                  |
|----------|-----------|-------------------------------------|
| Router   | 1         | PT-Router / Cisco 2911 (with FastEthernet modules) |
| Switch   | 4         | Switch-PT (Generic) / Cisco 2960    |
| Server   | 1         | Server-PT                           |
| PC       | 6         | PC-PT (End Devices)                 |

---

## ⚙️ Key Configuration Details

### 1. End Device IP Assignment

All PCs and the Server use **static IP addresses**.  
The **DNS Server** address for all devices is the Server’s IP: `192.168.1.100`.

| Component         | IP Address      | Subnet Mask     | Default Gateway | DNS Server     |
|-------------------|----------------|-----------------|----------------|----------------|
| Server0           | 192.168.1.100  | 255.255.255.0   | 192.168.1.1    | 192.168.1.100  |
| PC0 (Admin)       | 192.168.2.3    | 255.255.255.0   | 192.168.2.1    | 192.168.1.100  |
| PC2 (Accounts)    | 192.168.3.3    | 255.255.255.0   | 192.168.3.1    | 192.168.1.100  |
| PC4 (IT)          | 192.168.4.3    | 255.255.255.0   | 192.168.4.1    | 192.168.1.100  |

---

### 2. Router Configuration

The following IP addresses are configured on the router’s physical interfaces and enabled using the `no shutdown` command.

| Router Interface | IP Address     | Subnet Mask     |
|------------------|----------------|-----------------|
| Fa1/0 (or equivalent) | 192.168.1.1 | 255.255.255.0   |
| Fa0/0 (or equivalent) | 192.168.2.1 | 255.255.255.0   |
| Fa0/1 (or equivalent) | 192.168.3.1 | 255.255.255.0   |
| Fa1/1 (or equivalent) | 192.168.4.1 | 255.255.255.0   |

---

### 3. Server Service Configuration

The following services are enabled on **Server0 (192.168.1.100):**

| Service | Setting | Details |
|----------|----------|----------|
| **DNS** | ON | Entry Name: `www.google.com` → IP: `192.168.1.100` |
| **HTTP/HTTPS** | ON | Default Web Service Enabled |

---

## ✅ Verification

### 🔹 Inter-Network Ping Test  
Successful ping from any PC (e.g., **PC0**) to a device in a different network (e.g., **PC2** or **Server0**) confirms successful static routing through the router.

### 🔹 Web Connectivity Test  
Opening the web browser on any PC and navigating to the configured DNS name (**www.google.com**) confirms that both **DNS resolution** and **HTTP services** are correctly configured and accessible across subnets.

---

### 📄 Notes
- Ensure all router interfaces are enabled using `no shutdown`.  
- Verify that each PC is connected to the correct switch and VLAN.  
- Use the **Simulation Mode** in Packet Tracer to observe ICMP and DNS packet flow for learning purposes.

---

**Author:** _Hemang Ganjsinghani_  
**Tool:** Cisco Packet Tracer  
**Version:** v1.0  

