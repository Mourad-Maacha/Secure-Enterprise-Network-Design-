# 🧩 Network Design and Beautification  
### Part 1 – Enterprise Network Project (Mourad Innovations Inc)

This document outlines the **network design and beautification phase** for the Mourad Innovations Inc Enterprise Network.  
The goal is to logically design the topology in Cisco Packet Tracer before moving to full implementation and configuration.

---

## 🛰️ 1. ISP Routers

Place **two routers** to represent the two Internet Service Providers (ISPs):  
- SEACOM  
- SAFARICOM  

<img width="550" alt="Screenshot 2025-11-06 094201" src="https://github.com/user-attachments/assets/46873873-5f54-4c9e-989f-452d5543c8ae" />

---

## 🔥 2. Cisco ASA Firewalls

Add **two Cisco ASA firewalls (5500-X Series)** for security and redundancy between the ISPs and the internal network.

<img width="550" alt="Screenshot 2025-11-06 094409" src="https://github.com/user-attachments/assets/8b0b7be7-dd78-44dd-a211-604bf6db2305" />

---

## 🖧 3. Core (Multilayer) Switches

Next, add **two multilayer switches (Catalyst 3650)** to serve as the network’s core.  
These will handle **routing, inter-VLAN communication, and redundancy**.

<img width="550" alt="Screenshot 2025-11-06 094517" src="https://github.com/user-attachments/assets/0c9cfb6b-5106-44ae-8d04-185fe6a86607" />

---

## 🏢 4. Departmental Floor Design

Since the new building has **three floors**, assign departments and switches accordingly:

### Floor 1
- Sales & Marketing  
- Human Resources & Logistics  
→ Each department receives one dedicated switch.

### Floor 2
- Finance & Accounts  
- Administration & Public Relations  
→ Each department receives one switch.

### Floor 3
- ICT Department (Network, Systems, Cybersecurity, Developers, Support, etc.)  
- Server Room (Internal servers and controllers)  
→ Each has one dedicated switch.

<img width="550" alt="Screenshot 2025-11-06 095336" src="https://github.com/user-attachments/assets/d2375919-8743-4e64-8906-0cbc9dae0646" />

---

## ⚡ 5. Redundant Wiring and EtherChannel

Wire the network **from top to bottom**, starting with the ISP routers, firewalls, and multilayer switches.  
Implement **EtherChannel** between the two multilayer switches to ensure **redundancy and load balancing**.
> Tip: When wiring, always try to keep the ports consistent as this will help us in the configuration later on.

<img width="550" alt="Screenshot 2025-11-06 095828" src="https://github.com/user-attachments/assets/09fbe1f5-1403-4450-9056-e2e1c4ae9d7a" />

---

## 💻 6. Host Devices and Wireless Infrastructure

Add host devices to each department:
- PCs, Printers, VoIP Phones, Laptops, Tablets, and Smartphones  
- Replace each laptop’s Ethernet module with a **Wireless Module** (disable first).  
- Add and power on a **Lightweight Access Point (LAP)** per department.

Copy and replicate this setup across all departments **except the Server Room**.

<img width="550" alt="Screenshot 2025-11-06 100950" src="https://github.com/user-attachments/assets/60d5d9de-806a-44f2-b921-b4213bfcbd8d" />

---

## 🧠 7. Server Room and Controllers

Use the **last switch (Floor 3)** for **servers and controllers**:

### Servers:
- DHCP Server  
- DNS Server  
- Radius Server  

### Controllers:
- Wireless LAN Controller (WLC)  
- Cisco Voice Gateway (2811 Router)

> **Note:**  
> - The **WLC** should be in the same VLAN as all Lightweight Access Points (LAPs).  
> - The **Voice Gateway** should share the same VLAN as all IP Phones.

<img width="550" alt="Screenshot 2025-11-06 101957" src="https://github.com/user-attachments/assets/29f36484-7db4-462b-a68a-845ae4a13aee" />

---

## 🔒 8. DMZ Zone Connection

Connect the **DMZ zone** to **one firewall only** (left firewall).  
This introduces a **single point of failure** at the DMZ, consistent with real-world design considerations.

<img width="550" alt="Screenshot 2025-11-06 102506" src="https://github.com/user-attachments/assets/6e5f6b7e-b110-4170-83de-2cd34e158eff" />

---

## ☁️ 9. Cloud Integration

Simulate the cloud environment:
- Use a **Router 2911** and **bundle it into a cloud object**.  
- Add a **switch** and two **remote users** (from different countries) to the cloud network.  
- Cluster the switch and router as one unified cloud connection.

<img width="550" alt="Screenshot 2025-11-06 103013" src="https://github.com/user-attachments/assets/40ebc9b6-9044-4b68-9845-24367bb1f7f5" />


---

## 🏷️ 10. Device Naming and Final Layout

Ensure **all devices are properly named** according to their roles and locations.

Example naming convention:
- `FW1`, `FW2`  
- `Core-SW1`, `Core-SW2`  
- `F1-Sales-SW`, `F2-Finance-SW`, `F3-ServerRoom-SW`  
- `DHCP-SRV`, `DNS-SRV`, `RADIUS-SRV`, `WLC`, `Voice-GW`

<img width="550" alt="Screenshot 2025-11-06 104053" src="https://github.com/user-attachments/assets/557dec85-adc3-4186-853f-84f5f332d83a" />

---

## 🎨 11. Beautification and Documentation

Complete the **beautification phase** by:
- Applying color-coded borders for departments, DMZ, and external zones.  
- Adding **text comments** and **annotations** describing device roles.  
- Organizing layout for clarity and readability.

<img width="1071" height="647" alt="Screenshot 2025-11-07 085422" src="https://github.com/user-attachments/assets/fcb009ea-4edb-41de-b303-78b28a250aac" />

---

> ✅ **End of Step 1: Network Design and Beautification**  
Proceed to Step 2: [Basic Settings to All Devices + SSH + Standard ACL for SSH](2_Basic_Settings_SSH_and_ACL.md)
