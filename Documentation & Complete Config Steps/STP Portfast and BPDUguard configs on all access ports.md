# 🧩 Step 4 — STP Portfast & BPDUguard Configuration

## 🔍 Explanation

**Spanning Tree Protocol (STP) Portfast** and **Bridge Protocol Data Unit (BPDU) Guard** are crucial for improving performance and maintaining security on access layer switches.

- **Portfast**: Allows switch ports connected to end devices (like PCs, printers, or servers) to skip the usual 30-second listening/learning phase and transition to the forwarding state immediately.  
  > Example: When you unplug and plug a device back in, the port goes amber for ~30 seconds before going green. Portfast fixes that delay, improving network productivity.

- **BPDUguard**: Works with Portfast to protect against accidental loops. If a BPDU (a spanning-tree control message) is received on a Portfast-enabled port, the port is automatically shut down to prevent topology issues.

> ⚠️ **Important:** Only enable Portfast and BPDUguard on *access ports* — never on trunk ports.

---

## 🖥️ Configuration Steps

### 🧱 Server Department Switch

We’ll configure Portfast and BPDUguard on every access port. Remember that **f0/7** is trunked (connected to the Cisco Voice Gateway), so skip it.

```bash
conf t
int range f0/3-6, f0/8-24
spanning-tree portfast
spanning-tree bpduguard enable
do wr
```
---

## 🏢 All Other Access Switches
For all other switches (MK-SW, HL-SW, FIN-SW, ADMIN-SW, ICT-SW), apply Portfast and BPDUguard to every access port.

```bash
conf t
int range f0/3-24
spanning-tree portfast
spanning-tree bpduguard enable
do wr
```

## 🔐 DMZ Switch
Configure all ports (1–24) on the DMZ switch with Portfast and BPDUguard.

```bash
conf t
int range f0/1-24
spanning-tree portfast
spanning-tree bpduguard enable
do wr
```

## ✅ Step 4 Completed
All access switches are now configured with STP Portfast and BPDUguard, ensuring faster port activation and improved protection from accidental network loops.

Proceed to the next step:
👉 [[5. EtherChannel]]
