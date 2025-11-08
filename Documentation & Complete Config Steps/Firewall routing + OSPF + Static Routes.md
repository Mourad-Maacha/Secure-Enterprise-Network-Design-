# Step 12 — Firewall Routing: OSPF + Static Routes

## Overview
Each firewall will advertise its directly connected networks using **OSPF** and will also include **static routes** for redundancy.  
We’ll configure **primary** and **backup default routes**, then set up **OSPF area 0**.

---

## 🔹 FW1 Configuration

### Static Routes
Default route via ISP1 and a backup via ISP2 (with administrative distance 70):
```bash
conf t
route OUTSIDE1 0.0.0.0 0.0.0.0 105.100.50.1
route OUTSIDE2 0.0.0.0 0.0.0.0 197.200.100.1 70
end
write memory
```

OSPF Configuration:
```bash
conf t
router ospf 35
router-id 1.1.8.8
network 105.100.50.0 255.255.255.252 area 0
network 197.200.100.0 255.255.255.252 area 0
network 10.11.11.0 255.255.255.224 area 0
network 10.2.2.0 255.255.255.252 area 0
network 10.2.2.8 255.255.255.252 area 0
end
write memory
```

## 🔹 FW2 Configuration
Static Routes
```bash
conf t
route OUTSIDE2 0.0.0.0 0.0.0.0 197.200.100.5
route OUTSIDE1 0.0.0.0 0.0.0.0 105.100.50.5
end
```

OSPF Configuration:
```bash
conf t
router ospf 35
router-id 1.1.9.9
network 197.200.100.4 255.255.255.252 area 0
network 105.100.50.4 255.255.255.252 area 0
network 10.2.2.4 255.255.255.252 area 0
network 10.2.2.12 255.255.255.252 area 0
end
write memory
```

