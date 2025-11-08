# Step 14 — Network Testing (DHCP & ACL Verification)

## Overview
Before moving forward, it’s crucial to **test** the network configuration to ensure that:
- DHCP is functioning correctly.
- ACLs and NAT are properly allowing traffic.
- Routing and IP addressing across zones are correct.

This step will validate the setup by testing **DHCP**, **pings**, and **connectivity** between zones (Inside, DMZ, and Outside).

---

## 🧠 Test 1: DHCP Verification

We’ll start by verifying that devices are receiving IP addresses from the **DHCP server**.

1. Go to a **PC in the Sales & Marketing Room**.
2. Open the **Desktop tab → IP Configuration → Select DHCP**.
3. It's requesting an Ip Address:

<img width="550" alt="Pasted image 20251107131634" src="https://github.com/user-attachments/assets/6c28b3c4-c2f2-4a23-9cc8-2a5b226df07c" />

4. DHCP successfully assigns the correct IP address:

<img width="550" alt="Pasted image 20251107131744" src="https://github.com/user-attachments/assets/df89f44a-859d-41ea-9478-181504def3ae" />

✅ **Result:** DHCP is working correctly.

---

## 🧠 Test 2: Ping the Algeria Network

Next, we’ll test connectivity by attempting to ping the **Algeria computer** (or its network ID).

- From the same Sales & Marketing PC, run a **ping** command to the **Algeria network**.

<img width="550" alt="Pasted image 20251107133747" src="https://github.com/user-attachments/assets/4bf927f8-bf7a-414d-8e09-f5f146af0b38" />

❌ The ping **failed**.

After reviewing the network topology, we identified the issue:
- The **cloud router** had:
  - No IP address assigned to the interface connected to the switch.
  - **Duplicate IP addresses** on both ISP-facing interfaces (`20.20.20.1` and `30.30.30.1`).
  
In real-world conditions, the cloud would be external and beyond direct control, but here we’ll fix the addressing conflict manually.

---

## ⚙️ Fixing the Cloud Router Configuration

Apply the following commands on the **cloud router** to resolve the IP addressing issues:

```bash
conf t
int g0/2
ip address 8.0.0.1 255.0.0.0
no shut

int g0/0
no ip address 20.20.20.1 255.255.255.252
ip address 20.20.20.2 255.255.255.252
no shut

int g0/1
no ip address 30.30.30.1 255.255.255.252
ip address 30.30.30.2 255.255.255.252
no shut
end

write
```

## 🧪 Test 3: Re-Ping the Algeria Network
After applying the fix, repeat the ping test.

<img width="550" alt="Pasted image 20251107134047" src="https://github.com/user-attachments/assets/d7027bb0-38a1-405a-870f-ad8b134756f0" />

✅ This time, the ping succeeded!

## 🧪 Test 4: Ping the DMZ Devices
Finally, test connectivity to devices located in the DMZ.

<img width="550" alt="Pasted image 20251107134426" src="https://github.com/user-attachments/assets/83d7e66b-74f3-4274-a33f-1813fddb86d1" />

## ✅ 5. **Step Completion**
✅ Summary
| Test         | Description                                                 | Result   |
| ------------ | ----------------------------------------------------------- | -------- |
| DHCP         | Verified IP assignment from DHCP server                     | ✅ Passed |
| Ping Algeria | Initial failure due to IP conflict, fixed via router config | ✅ Passed |
| Ping DMZ     | Successful communication                                    | ✅ Passed |

Next Step → 15. Wireless Network Configurations
