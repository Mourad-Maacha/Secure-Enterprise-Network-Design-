# Step 13 — Firewall Inspection Policy Configuration

## Overview
This step is **critical** — without proper firewall configuration, nothing will function.  
We’ll enable **NAT** and **inspection policies** to allow selective communication between zones.  
- The **DMZ** will have access to outside resources.
- Internal (inside) servers **will not** have internet access.
- Configuration applies to **both firewalls**.

---

## 🔹 FW1 Configuration
### NAT Configuration
Before applying NAT, we must create object networks for each zone relationship.

```bash
conf t
object network INSIDE1-OUTSIDE1
subnet 172.16.0.0 255.255.0.0
nat (INSIDE1,OUTSIDE1) dynamic interface
exit

object network INSIDE2-OUTSIDE1
subnet 172.16.0.0 255.255.0.0
nat (INSIDE2,OUTSIDE1) dynamic interface
exit

object network INSIDEWLAN1-OUTSIDEWLAN1
subnet 10.20.0.0 255.255.0.0
nat (INSIDE1,OUTSIDE1) dynamic interface
exit

object network INSIDEWLAN2-OUTSIDEWLAN1
subnet 10.20.0.0 255.255.0.0
nat (INSIDE2,OUTSIDE1) dynamic interface
exit

object network INSIDE1-OUTSIDE2
subnet 172.16.0.0 255.255.0.0
nat (INSIDE1,OUTSIDE2) dynamic interface
exit

object network INSIDE2-OUTSIDE2
subnet 172.16.0.0 255.255.0.0
nat (INSIDE2,OUTSIDE2) dynamic interface
exit

object network INSIDEWLAN1-OUTSIDEWLAN2
subnet 10.20.0.0 255.255.0.0
nat (INSIDE1,OUTSIDE2) dynamic interface
exit

object network INSIDEWLAN2-OUTSIDEWLAN2
subnet 10.20.0.0 255.255.0.0
nat (INSIDE2,OUTSIDE2) dynamic interface
exit

object network DMZ-OUTSIDE1
subnet 10.11.11.0 255.255.255.224
nat (DMZ,OUTSIDE1) dynamic interface
exit

object network DMZ-OUTSIDE2
subnet 10.11.11.0 255.255.255.224
nat (DMZ,OUTSIDE2) dynamic interface
end

write memory
```

## 🔹 FW2 Configuration
### NAT Configuration
```bash
conf t
object network INSIDE1-OUTSIDE1
subnet 172.16.0.0 255.255.0.0
nat (INSIDE1,OUTSIDE1) dynamic interface
exit

object network INSIDE2-OUTSIDE1
subnet 172.16.0.0 255.255.0.0
nat (INSIDE2,OUTSIDE1) dynamic interface
exit

object network INSIDEWLAN1-OUTSIDEWLAN1
subnet 10.20.0.0 255.255.0.0
nat (INSIDE1,OUTSIDE1) dynamic interface
exit

object network INSIDEWLAN2-OUTSIDEWLAN1
subnet 10.20.0.0 255.255.0.0
nat (INSIDE2,OUTSIDE1) dynamic interface
exit

object network INSIDE1-OUTSIDE2
subnet 172.16.0.0 255.255.0.0
nat (INSIDE1,OUTSIDE2) dynamic interface
exit

object network INSIDE2-OUTSIDE2
subnet 172.16.0.0 255.255.0.0
nat (INSIDE2,OUTSIDE2) dynamic interface
exit

object network INSIDEWLAN1-OUTSIDEWLAN2
subnet 10.20.0.0 255.255.0.0
nat (INSIDE1,OUTSIDE2) dynamic interface
exit

object network INSIDEWLAN2-OUTSIDEWLAN2
subnet 10.20.0.0 255.255.0.0
nat (INSIDE2,OUTSIDE2) dynamic interface
end

write memory
```

## 🔹 Firewall Inspection Policies (ACLs)
To permit necessary traffic (ICMP, Web, DNS), we’ll create access control lists (ACLs).
These define which services are allowed between zones.

### FW1
```bash
conf t
access-list RES extended permit icmp any any
access-list RES extended permit tcp any any eq 80
access-list RES extended permit tcp any any eq 53
access-list RES extended permit udp any any eq 53
access-group RES in interface DMZ
access-group RES in interface OUTSIDE1
access-group RES in interface OUTSIDE2
end

write memory
```

### FW2
```bash
conf t
access-list RES extended permit icmp any any
access-list RES extended permit tcp any any eq 80
access-list RES extended permit tcp any any eq 53
access-list RES extended permit udp any any eq 53
access-group RES in interface OUTSIDE1
access-group RES in interface OUTSIDE2
end

write memory
```

