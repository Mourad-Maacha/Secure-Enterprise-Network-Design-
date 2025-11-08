# Step 11 — Firewall Interface Security Zones and Levels

In this step, we will configure the **firewall interfaces**, assign them to **zones**, and define their **security levels**.  
This is a crucial step — if the firewalls aren’t correctly configured, **nothing else in the network will function properly.**

---

## 🔍 Understanding Firewall Zones

Before configuring, let’s **logically imagine the zones** of our perimeter firewalls.

### Zone Overview

- **DMZ** → Hosts public-facing servers  
- **INSIDE** → Connects to the internal Layer 3 switches  
- **OUTSIDE** → Connects to the ISP routers  

### Visual Representation

Here’s a simplified sketch of how zones are arranged:

<img width="550" alt="Pasted image 20251107114448" src="https://github.com/user-attachments/assets/3174905c-bab4-4523-a490-f7dcc2b978e6" />

### Interface Mapping

#### 🔹 PERIMETER-FW1

| Interface | Zone Name | Connection | Security Level |
|------------|------------|-------------|----------------|
| g1/1–2 | OUTSIDE | ISPs | 0 |
| g1/3–4 | INSIDE | CORE-SWs | 100 |
| g1/5 | DMZ | DMZ Switch | 70 |

#### 🔹 PERIMETER-FW2

| Interface | Zone Name | Connection | Security Level |
|------------|------------|-------------|----------------|
| g1/1–2 | OUTSIDE | ISPs | 0 |
| g1/3–4 | INSIDE | CORE-SWs | 100 |
| — | — | No DMZ connection | — |

---

## 🧱 Firewall Configuration

### ⚙️ PERIMETER-FW1

1. Access the firewall.
   - When prompted for a password, simply press **Enter** (default is blank).
2. Enter global configuration mode and apply the following:

```bash
conf t
hostname FW1

int g1/3
no shut
ip address 10.2.2.2 255.255.255.252
nameif INSIDE1
security-level 100

int g1/4
no shut
ip address 10.2.2.10 255.255.255.252
nameif INSIDE2
security-level 100
exit

int g1/5
no shut
ip address 10.11.11.1 255.255.255.224
nameif DMZ
security-level 70
exit

int g1/1
no shut
ip address 105.100.50.2 255.255.255.252
nameif OUTSIDE1
security-level 0
exit

int g1/2
no shut
ip address 197.200.100.2 255.255.255.252
nameif OUTSIDE2
security-level 0
exit

end
write memory
```

### ⚙️ PERIMETER-FW2
This firewall has no DMZ interface, so we only configure Inside and Outside zones.

Commands:
```bash
conf t

int g1/3
no shut
ip address 10.2.2.6 255.255.255.252
nameif INSIDE1
security-level 100
exit

int g1/4
no shut
ip address 10.2.2.14 255.255.255.252
nameif INSIDE2
security-level 100
exit

int g1/1
ip address 105.100.50.6 255.255.255.252
nameif OUTSIDE1
security-level 0
no shut
exit

int g1/2
ip address 197.200.100.6 255.255.255.252
nameif OUTSIDE2
security-level 0
no shut
exit

end
write memory
```

> 🧠 Notes
>  Traffic cannot flow from lower security levels to higher security levels by default.
>  The firewall will block such traffic unless explicitly allowed by ACLs or inspection rules (to be configured later).

