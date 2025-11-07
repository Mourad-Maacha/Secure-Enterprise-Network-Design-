# 🏢 Enterprise Network Design & Implementation
<img width="2369" alt="Mourad_Maacha_Secure_Company_Project_Topology" src="https://github.com/user-attachments/assets/2f49b759-732f-4f44-aee7-08e155f81c00" />

## 🔧 Project Overview

This project represents an **advanced enterprise-level network design and implementation** created in **Cisco Packet Tracer**. It simulates the full infrastructure of a large-scale organization — **Mourad Innovations Inc**, a global provider of innovative **cloud-based solutions** with a focus on **creativity, agility, and customer-centricity**.

The organization employs over **600 staff members** and is expanding into a **new three-story headquarters**. The building includes departments such as:

- Sales & Marketing  
- Human Resources & Logistics  
- Finance & Accounts  
- Administration & Public Relations  
- ICT Department & Server Room  

Within the **ICT department**, specialized teams include Software Developers, Cloud Engineers, Cybersecurity Engineers, Network Engineers, System Administrators, IT Support Specialists, Business Analysts, and Project Managers.

---

## 🛡️ Network Security and Architecture

The network is designed with **multiple layers of security**, **redundancy**, and **high availability** to ensure continuous operations and data protection.

### Key Security Measures
- **Firewall Zones:** Outside, Inside, and DMZ for network segmentation.  
- **DMZ Servers:** Public-facing services (FTP, Web, Email, App, NAS) are hosted in the DMZ.  
- **Internal Servers:** DHCP, DNS, Radius, and Active Directory servers reside in the inside zone for secure internal access.  
- **Comprehensive Policy Enforcement:** The firewall defines access control, routing, and inspection rules to safeguard internal resources.

---

## 🧩 Core Infrastructure Components

| Component | Description |
|------------|-------------|
| **ISP Connectivity** | Dual ISPs (SEACOM & Safaricom) for redundant internet access |
| **Firewalls** | Two Cisco ASA 5500-X firewalls for network security and redundancy |
| **Core & Access Switching** | Catalyst 3850 (L3) and 2960 (L2) switches for high-speed LAN |
| **Routing** | Implemented on firewalls and multilayer switches |
| **Virtualization** | Two physical servers hosting multiple VMs for critical services |
| **Wireless** | Cisco WLC managing multiple LAPs across all departments |
| **VoIP** | Cisco Voice Gateway for enterprise telephony service |

---

## ☁️ Cloud & Connectivity

The network supports **cloud computing integration**, allowing global access to corporate resources and client-facing cloud services.  
This ensures that the Mourad Innovations team can collaborate, deploy, and manage systems efficiently from anywhere in the world.

---

## ⚙️ Network Requirements and Design Goals

### **Performance & Reliability**
- High-performance design with redundancy and scalability
- Hierarchical model ensuring resilience and fault tolerance

### **Addressing Plan**
| Network | Address Range |
|----------|----------------|
| Management | 192.168.10.0/24 |
| WLAN | 10.20.0.0/16 |
| LAN | 172.16.0.0/16 |
| VoIP | 172.30.0.0/16 |
| DMZ | 10.11.11.0/27 |
| Public (SEACOM) | 105.100.50.0/30 |
| Public (Safaricom) | 197.200.100.0/30 |

---

## 🧠 Technical Implementation Highlights

- **Platform:** Cisco Packet Tracer  
- **ISPs:** Dual connectivity for redundancy  
- **VLANs:**  
  - VLAN10: Management  
  - VLAN20: LAN  
  - VLAN50: WLAN  
  - VLAN70: VoIP  
  - VLAN199: Blackhole (unused ports)  
- **EtherChannel (LACP):** Link aggregation for bandwidth efficiency  
- **HSRP:** High Availability and Failover between Core Switches  
- **Inter-VLAN Routing:** Configured on Layer 3 switches  
- **DHCP:** Centralized dynamic IP allocation  
- **Static IPs:** Assigned to DMZ and server room devices  
- **STP Configuration:** PortFast + BPDU Guard on all access ports  
- **OSPF:** Routing between firewalls, routers, and L3 switches  
- **ACL for SSH:** Restricted remote admin access to authorized PCs only  
- **Cisco ASA Firewall:** Configured for routing, zones, and inspection policies  
- **VoIP:** Fully configured voice gateway with internal dial plan  
- **Wireless:** Centralized AP management through WLC  
- **Final Testing:** Full connectivity and redundancy validation

---

## ✅ Project Goals

- Achieve **maximum uptime**, **redundancy**, and **security**
- Ensure **cross-department connectivity** with VLAN and OSPF integration  
- Provide a **scalable design** suitable for enterprise-level expansion  
- Demonstrate mastery of **advanced Cisco configurations** within a simulated environment  

---

## 📸 Project Assets

- `Mourad_Innovations_Enterprise_Network.pkt` – Cisco Packet Tracer Project File  
- `Assets/Topology_Screenshots/` – Network topology and device layout images  
- `Documentation/` – Full configuration notes and setup steps  

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).

---

### 👨‍💻 Author
**Mourad Maacha**  
*Network & Cybersecurity Engineer*  
[GitHub Profile](https://github.com/Mourad-Maacha) • [LinkedIn](https://www.linkedin.com/in/mourad-maacha/)

---
