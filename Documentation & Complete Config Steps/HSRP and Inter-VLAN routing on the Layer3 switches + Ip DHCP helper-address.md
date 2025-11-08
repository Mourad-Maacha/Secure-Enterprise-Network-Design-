# 🧩 Step 7 — HSRP and Inter-VLAN Routing + DHCP Helper Addresses

Every department in the organization will receive IP addresses dynamically from the **DHCP server** located in the **Server Room**.  
We’ll now configure **Hot Standby Router Protocol (HSRP)** alongside **Inter-VLAN Routing** on the **Core (Layer 3) Switches** to ensure gateway redundancy and high availability.

---

## ⚙️ Overview

- **HSRP (Hot Standby Router Protocol)** provides a **virtual default gateway** shared between two routers (or Layer 3 switches).
- One device is **Active**, and the other is **Standby**.
- If the active router fails, the standby router automatically takes over — maintaining seamless network connectivity.
- **IP Helper Addresses** allow VLANs to forward DHCP requests to the DHCP Server.

---

## 🧠 HSRP and VLAN Role Plan

| VLAN / Department | Active Router (Core-SW1) | Standby Router (Core-SW2) | Gateway IP (.1) | Helper Address |
| ----------------- | ------------------------ | -------------------------- | ---------------- | --------------- |
| Management (10)   | Standby (.3)             | Active (.2)               | 192.168.10.1     | 10.11.11.38     |
| LAN (20)          | Standby (.3)             | Active (.2)               | 172.16.0.1       | 10.11.11.38     |
| WLAN (50)         | Active (.2)              | Standby (.3)              | 10.20.0.1        | 10.11.11.38     |
| Inside Servers (90) | Active (.34)            | Standby (.35)             | 10.11.11.33      | None (Static)   |

> Both Core Switches will serve as gateways — but the “Active” switch for each VLAN handles the actual routing unless it fails.

---

## 🧱 CORE-SW1 Configuration (Active for WLAN & Inside Servers)

```bash
conf t

interface Vlan10
 ip address 192.168.10.3 255.255.255.0
 ip helper-address 10.11.11.38
 standby 10 ip 192.168.10.1

interface Vlan20
 ip address 172.16.0.3 255.255.0.0
 ip helper-address 10.11.11.38
 standby 20 ip 172.16.0.1

interface Vlan50
 ip address 10.20.0.2 255.255.0.0
 ip helper-address 10.11.11.38
 standby 50 ip 10.20.0.1

interface Vlan90
 ip address 10.11.11.34 255.255.255.224
 standby 90 ip 10.11.11.33

exit
do wr
```
Here's what the config looks like:

<img width="330" alt="Screenshot 2025-11-07 100737" src="https://github.com/user-attachments/assets/4236b596-12b8-4616-ad83-0fb15d31fa0d" />

## 🧱 CORE-SW2 Configuration (Active for MGT & LAN)
```bash
conf t

interface Vlan10
 ip address 192.168.10.2 255.255.255.0
 ip helper-address 10.11.11.38
 standby 10 ip 192.168.10.1

interface Vlan20
 ip address 172.16.0.2 255.255.0.0
 ip helper-address 10.11.11.38
 standby 20 ip 172.16.0.1

interface Vlan50
 ip address 10.20.0.3 255.255.0.0
 ip helper-address 10.11.11.38
 standby 50 ip 10.20.0.1

interface Vlan90
 ip address 10.11.11.35 255.255.255.224
 standby 90 ip 10.11.11.33

exit
do wr
```
## 🔍 Verifying HSRP Status
Once configuration is complete, run the following command on both switches to verify status:

```bash
show standby brief
```
🖼️ Example Output:

<img width="550" alt="Screenshot 2025-11-07 101601" src="https://github.com/user-attachments/assets/548da449-ae5e-4d81-9d63-5dd36ff64a73" />
