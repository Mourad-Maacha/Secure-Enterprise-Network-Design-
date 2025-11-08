# 🧩 Step 15 — Wireless Network Configurations

Let's set up and test our Wireless LAN Controller (WLC) and access points to provide Wi-Fi across the network.

---

### 🖥️ 1. Initial Setup

- Add a new PC next to the **Wireless LAN Controller (WLC)**.
- Plug it into the same network and assign it an IP address in the same range as the WLC.
- Like this:

<img width="550" alt="Pasted image 20251107140319" src="https://github.com/user-attachments/assets/19a2ef8a-1248-4bfc-bbf7-339f30ddd15a" />

- Make sure you can **ping** the WLC from this PC.
- Then go to **Desktop > Web Browser** and input the **Default Gateway** to start configuration.

---

### ⚙️ 2. Configure the Wireless LAN Controller

Before opening the browser, configure the WLC manually:

- Click the **WLC device**, go to **Management**, and fill out the following:

<img width="550" alt="Pasted image 20251107140645" src="https://github.com/user-attachments/assets/52199ac0-2d53-4ccc-9da8-a4be47de852d" />

- On the PC’s browser, enter the WLC IP address: `10.20.0.10`

You should see this screen:

<img width="550" alt="Pasted image 20251107140738" src="https://github.com/user-attachments/assets/c0260597-45c8-43c6-97c7-53d7052fe86f" />


- Create an admin account:
  - **Username:** `cisco`
  - **Password:** `Cisco123456`

---

### 🧾 3. System Information

Fill out the setup form:

| Field | Value |
|--------|--------|
| **System Name** | Mourad-WLC |
| **Management IP Address** | 10.20.0.10 |
| **Subnet Mask** | 255.255.0.0 |
| **Default Gateway** | 10.20.0.1 |

Then click **Next**.

<img width="550" alt="Pasted image 20251107141121" src="https://github.com/user-attachments/assets/e7af55ea-6247-4cc7-a23d-900d085c92bc" />

---

### 📶 4. WLAN Setup Wizard

- Fill in the **Network Names** and **Passphrases**, then click **Next** twice.
- Review everything and click **Apply**.
- The page will reload and appear stuck on this screen — **don’t wait**; it’s normal:

<img width="550" alt="Pasted image 20251107141439" src="https://github.com/user-attachments/assets/a88a13c5-9836-4886-b50c-a9403c98c1d5" />

- Just close the browser.

---

### 🔁 5. Verify Reboot

- In the **Command Prompt**, ping `10.20.0.10` again.

<img width="550" alt="Pasted image 20251107141558" src="https://github.com/user-attachments/assets/d78e9002-8d0b-4116-bb35-47812006bfa4" />

- If it responds, the WLC rebooted successfully.
- Go back to the **Web Browser**, this time using `https://10.20.0.10`.

You’ll be asked to log in:

<img width="550" alt="Pasted image 20251107141727" src="https://github.com/user-attachments/assets/a7f9e820-d2bd-4bd1-984b-4c824aa87f17" />

---

### 📡 6. Create WLANs

Now that we’re logged in, we’ll create **4 Wi-Fi networks**:  
**Employees, Guests, Auditors, and Corporate.**

- Go to **WLANs > Click Go**.
- Fill in the details:

| Profile Name | SSID | Security | Notes |
|---------------|------|-----------|--------|
| AUDITORS WIFI | AUDITORS | WPA2-PSK | WPA2 Policy Enabled |
| CORPORATE WIFI | CORPORATE | WPA2-PSK | WPA2 Policy Enabled |
| GUEST WIFI | GUEST | WPA2-PSK | WPA2 Policy Enabled |

Example:

<img width="550" alt="Pasted image 20251107142638" src="https://github.com/user-attachments/assets/1bdc53aa-b83d-4cc1-9d78-1043fc8951b0" />

Security settings:

<img width="550" alt="Pasted image 20251107142329" src="https://github.com/user-attachments/assets/d34006dd-781a-47e2-8c0e-e71ea5425c04" />


Once done, you should see:

<img width="550" alt="Pasted image 20251107143003" src="https://github.com/user-attachments/assets/ce01f315-a6a2-416a-87bd-7399d081a2ff" />

Finally, click **Save Configuration**.

---

### 📲 7. Verify Access Points

Hover over your **LAP-PT** to confirm WLAN broadcasting:

<img width="550" alt="Pasted image 20251107143338" src="https://github.com/user-attachments/assets/93f34dfc-6da8-44fa-b856-8ca905ddfda4" />


You should see all 4 SSIDs being advertised.

---

### 🧪 8. Testing Wireless Devices

- Go to the **Laptop** in the Sales & Marketing room.
- Navigate to **Config > Wireless0**.
- Change **SSID** to `CORPORATE`.
- Select **WPA2-PSK**, enter the password, and close.
- You’ll see it connected to a LAP (not necessarily the one nearby — normal behavior).

<img width="550" alt="Pasted image 20251107144243" src="https://github.com/user-attachments/assets/e94a8461-5fb5-48b8-870f-e212488e3425" />

Repeat this process for all wireless devices.

Here’s what the full topology looks like when all are connected:

<img width="2369" height="1293" alt="Topology Wireless" src="https://github.com/user-attachments/assets/ff24de7a-932a-4afc-895b-1748766cfb64" />


> Turn on **DHCP** on all wireless devices — they should each receive IP addresses.

---
