# 🧩 Step 3 – VLAN Assignment + Access & Trunk Port Configuration  
### Enterprise Network Project (Mourad Innovations Inc)

In this step, we’ll configure **VLANs**, **access ports**, and **trunk ports** on both **Layer 2** and **Layer 3 switches**, ensuring consistent cabling and logical segmentation across the enterprise network.

---

## 🧱 Layer 2 Switches

We’ll begin with the **Layer 2 access switches**.  
The first step is to **trunk** the ports connecting to the **multilayer (L3) switches**.

---

### 🔹 Example: MK-SW (Sales & Marketing Switch)

#### 1. Trunk Ports (to multilayer switches):
```bash
config t
int range f0/1-2
switchport mode trunk
```

#### 2. Create Vlans and name them:
```bash
vlan 10
name MGT
vlan 20
name LAN
vlan 50
name WLAN
vlan 70
name VoIP
vlan 199
name BLACKHOLE
exit
```

#### 3. VLAN Port Assignments
| Device             | Port   | VLAN    | Description           |
| :----------------- | :----- | :------ | :-------------------- |
| MK-PC, MK-PR       | f0/3-4 | VLAN 20 | LAN devices           |
| MK-VoIP1, MK-VoIP2 | f0/5-6 | VLAN 70 | IP Phones             |
| MK-LAP             | f0/7   | VLAN 50 | Wireless Access Point |

#### Assign Vlans Accordingly

```bash
int range f0/3-4
switchport mode access
switchport access vlan 20

int range f0/5-6
switchport mode access
switchport access vlan 70

int f0/7
switchport mode access
switchport access vlan 50
```

#### 4. Blackhole VLAN for Unused Ports
> For better security, shut down all unused interfaces and assign them to VLAN 199.

```bash
int range f0/8-24, g0/1-2
switchport mode access
switchport access vlan 199
shutdown

do wr
exit
```

> If cabling is consistent across your topology, you can copy-paste this same configuration to other access switches (MK-SW, HL-SW, FIN-SW, ADMIN-SW, ICT-SW).

---

## 📄 Full Configuration Template for L2 Switches
Copy this configuration into any Layer 2 switch CLI (change hostname accordingly):

```bash
Config t
Int range f0/1-2
Switchport mode trunk
Exit

Vlan 10
Name MGT
Vlan 20
Name LAN
Vlan 50
Name WLAN
Vlan 70
Name VoIP
Vlan 199
Name BLACKHOLE
Exit

Int range f0/3-4
Switchport mode access
Switchport access vlan 20

Int range f0/5-6
Switchport mode access
Switchport access vlan 70

Int range f0/7
Switchport mode access
Switchport access vlan 50

Int range f0/8-24, g0/1-2
Switchport mode access
Switchport access vlan 199
Shut

Do wr
Exit
```

---

## 🖥️ Server Room Configuration (SERVER-SW)
For the Server Room Switch, VLAN 90 will be used for inside servers, and the blackhole VLAN will not apply here.
- Servers: VLAN 90
- Wireless LAN Controller: VLAN 50
- Voice Gateway: Trunked connection to support VoIP operations

Configuration:

```bash
int range f0/1-2, f0/7
switchport mode trunk
exit

int range f0/3-5
switchport mode access
switchport access vlan 90

int f0/6
switchport mode access
switchport access vlan 50

do wr
```

---

## 🧠 Layer 3 Switches
The Layer 3 switches will trunk connections to all Layer 2 switches and create the same VLANs for inter-VLAN routing later.
> Note: No blackhole VLANs are used on Layer 3 switches, since they’re physically secured and inaccessible to users.

Configuration:

```bash
conf t
int range g1/0/3-8
switchport mode trunk
exit

vlan 10
name MGT
vlan 20
name LAN
vlan 50
name WLAN
vlan 70
name VoIP
vlan 90
name INSIDE-SERVERS
exit

do wr
```
Repeat on both L3 switches.

## ☎️ VLAN 70 – VoIP Configuration
For VoIP VLANs, configure the ports as voice VLANs instead of standard data VLANs.
This allows IP phones to properly tag voice traffic for QoS and signaling.

Configuration:

```bash
conf t
int range f0/5-6
switchport voice vlan 70
exit

int range f0/5-6
no switchport access vlan 70

do wr
```
> Apply this to all departmental switches that host VoIP phones.
