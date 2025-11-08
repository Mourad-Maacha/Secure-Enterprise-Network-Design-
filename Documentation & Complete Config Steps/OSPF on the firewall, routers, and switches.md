# Step 10 — OSPF on the Firewall, Routers, and Switches
In this step, we’ll configure **OSPF (Open Shortest Path First)** routing across the Layer 3 switches and ISP routers to enable dynamic routing between all networks.  
Each device will use a **unique Router ID** to prevent conflicts.

---

## 🧩 L3 Switches OSPF Configuration
Both **CORE-SW1** and **CORE-SW2** participate in OSPF Area 0 (the backbone area).  
They will advertise all directly connected VLAN and point-to-point networks.

---

### 🖥️ CORE-SW1 Configuration
CORE-SW1 has six networks connected that need to be advertised via OSPF.

**Commands:**
```bash
conf t
router ospf 35
router-id 1.1.1.1
network 10.2.2.0 0.0.0.3 area 0
network 10.2.2.4 0.0.0.3 area 0
network 172.16.0.0 0.0.255.255 area 0
network 192.168.10.0 0.0.0.255 area 0
network 10.20.0.0 0.0.255.255 area 0
network 10.11.11.32 0.0.0.31 area 0
do wr
```

## 🖥️ CORE-SW2 Configuration
Commands:
```bash
conf t
router ospf 35
router-id 1.1.2.2
network 10.2.2.8 0.0.0.3 area 0
network 10.2.2.12 0.0.0.3 area 0
network 172.16.0.0 0.0.255.255 area 0
network 192.168.10.0 0.0.0.255 area 0
network 10.20.0.0 0.0.255.255 area 0
network 10.11.11.32 0.0.0.31 area 0
do wr
```

> ⚠️ Note: Each device must have a unique Router ID (RID).
> Example: CORE-SW1 → 1.1.1.1, CORE-SW2 → 1.1.2.2.

## 🌐 Routers OSPF Configuration
Each ISP and the cloud router will also run OSPF in Area 0 to establish dynamic routes between the internal and external networks.

### 🛰️ SEACOM-ISP Router

Commands:
```bash
conf t
router ospf 35
router-id 1.1.3.3
network 105.100.50.0 0.0.0.3 area 0
network 105.100.50.4 0.0.0.3 area 0
network 20.20.20.0 0.0.0.3 area 0
do wr
```

### 🌍 SAFARICOM-ISP Router

Commands:
```bash
conf t
router ospf 35
router-id 1.1.4.4
network 30.30.30.0 0.0.0.3 area 0
network 205.200.100.0 0.0.0.3 area 0
network 205.200.100.4 0.0.0.3 area 0
do wr
```

### ☁️ CLOUD Router

Commands:
```bash
conf t
router ospf 35
router-id 1.1.5.5
network 8.0.0.0 0.255.255.255 area 0
network 20.20.20.0 0.0.0.3 area 0
network 30.30.30.0 0.0.0.3 area 0
do wr
```
> After configuring OSPF on all devices, re-cluster the Cloud in Packet Tracer to simplify your topology view.

## ✅ OSPF is now fully configured across your network infrastructure.
You can now proceed to:
➡️ Step 11 — Firewall Interface Security Zones and Levels
