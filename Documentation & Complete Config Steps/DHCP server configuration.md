# Step 9 — DHCP Server Device Configurations

In this step, we’ll configure the **DHCP server** to automatically assign IP addresses to the devices in the **Management**, **LAN**, and **WLAN** networks.

---

## 🧩 Initial Setup

1. Open the **DHCP Server**:
   - Click on the **Server** device.
   - Go to the **Services** tab.
   - Select **DHCP**.
2. **Clear all existing data** so everything shows as `0`, then click **Save**.  
<img width="550" alt="Screenshot 2025-11-07 103858" src="https://github.com/user-attachments/assets/a410b3db-f3f9-4f2e-bf08-3763749b4b0c" />

---

## 🧱 Creating DHCP Pools

We’ll create **three separate DHCP pools** for each department network.

---

### 🖥️ Management Network (MGT-Pool)

| Field | Value |
|--------|--------|
| Pool Name | MGT-Pool |
| Default Gateway | 192.168.10.1 |
| DNS Server | 10.11.11.37 |
| Start IP Address | 192.168.10.11 |
| Subnet Mask | 255.255.255.0 |
| Maximum Number of Users | 200 |

After entering all details, click **Add**.  
Your settings should look like this:  
<img width="550" alt="Screenshot 2025-11-07 104304" src="https://github.com/user-attachments/assets/8197c404-396a-4465-bc74-a886883d5a06" />

---

### 🌐 LAN Network

Copy these exact settings in the DHCP configuration:  
<img width="550" alt="Screenshot 2025-11-07 104413" src="https://github.com/user-attachments/assets/98f121c4-a545-4a71-bc6d-286ff673f92b" />


---

### 📡 WLAN Network

Copy these settings for the WLAN DHCP pool:  
<img width="550" alt="Screenshot 2025-11-07 104641" src="https://github.com/user-attachments/assets/5e3a6cd6-8e95-4274-9f1c-d7c032738564" />


> ⚠️ Note: For the WLAN pool to work properly, you must add the **IP address of the Wireless LAN Controller (WLC)** —  
> **WLC IP Address: 10.20.0.10**

---

