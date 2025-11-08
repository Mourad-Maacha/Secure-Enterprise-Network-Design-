# 🔐 Step 2 – Basic Settings, SSH Configuration & Standard ACLs  
### Enterprise Network Project (Mourad Innovations Inc)

This step covers applying **basic configurations** to all switches, enabling **secure remote SSH management**, and creating a **Standard ACL** to restrict SSH access to the **Management Network (192.168.10.0/24)** only.

---

## 🧱 1. **Configuration Order**

Before you begin:

- The **firewall** will be configured last, once you understand all network devices and their interconnections.  
- Start configuration with the **DMZ switch**, followed by the **multilayer switches**, then move to all **departmental access switches**.  
- **ACLs** will ensure only the **management subnet** has SSH access to the devices.

---

## ⚙️ 2. **Basic Switch Configuration Template**

Below is the **standard configuration** to be applied to all switches.  
You can copy and paste it directly into the CLI of each switch using Cisco Packet Tracer.

> ⚠️ **Remember:** Change the `hostname` to match each switch (e.g., `SM-SW`, `HR-SW`, `FIN-SW`, etc.)

---

```bash
En
Conf t
Hostname DMZ-SW

Line console 0
Password cisco
Login
Logging synchronous
Exec-timeout 3 0
Exit

Enable password cisco
Banner motd !NO UNAUTHORISED ACCESS!
No ip domain-lookup

Service password-encryption

Username Cisco password Cisco
Ip domain-name cisco.com
Crypto key generate rsa general-keys modulus 1024
Ip ssh version 2

Line vty 0 15
Login local
Transport input ssh
Exit

Access-list 1 permit 192.168.10.0 0.0.0.255
Access-list 1 deny any

Line vty 0 15
Access-class 1 in
Exit

Do wr
```

---

## 🧩 3. **Key Configuration Highlights**

- **Hostname**: Identifies each switch by department or function.
- **Console & Enable Passwords**: Secures physical and privileged access.
- **Banner MOTD**: Displays a legal warning message on login.
- **SSH Configuration**: Provides secure encrypted management sessions.
- **Password Encryption**: Prevents plain-text password visibility.
- **ACL** (Access Control List):
  - Permits SSH access only from the Management Network (192.168.10.0/24).
  - Denies all other sources.

---

## 🚫 4. **Devices Excluded from This Step**

- **Firewalls**: Configuration will be completed at the end of the project for better context.
- **ISP Routers / Cloud**: No configuration at this stage (only OSPF testing later).

## ✅ 5. **Step Completion**

You’ve now:
- Applied basic security and management settings on all switches.
- Secured remote access with SSH.
- Restricted management access using a standard ACL.

> Continue to Step 3 → VLAN Assignment, Access & Trunk Port Configuration on L2 & L3 Switches
> In the next step, we’ll create VLANs, assign access ports, and configure trunk links across the network.
