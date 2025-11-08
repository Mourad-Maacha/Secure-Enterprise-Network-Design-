# Step 8 — Static IP Address Assignment

In this step, we’ll assign **static IP addresses** to all the servers located in both the **Servers Room** and the **DMZ Server Farm**.

---

## 🖥️ Servers Room

We’ll manually configure the following static IPs:

| Server  | IP Address    | Subnet Mask    | Notes |
|----------|---------------|----------------|--------|
| DHCP     | 10.11.11.38   | /27 (255.255.255.224) | DHCP service provider |
| DNS      | 10.11.11.37   | /27 (255.255.255.224) | Domain Name System server |
| RADIUS   | 10.11.11.36   | /27 (255.255.255.224) | Authentication server |

Each server will be configured through the **GUI** using the following settings:

- **DHCP Server**
  - Copy these settings:  
<img width="550" alt="Screenshot 2025-11-07 102401" src="https://github.com/user-attachments/assets/1a224ee8-f7b6-4186-83c8-55ade74da42d" />

- **DNS Server**
  - Copy these settings:  
<img width="550" alt="Screenshot 2025-11-07 102722" src="https://github.com/user-attachments/assets/52b1a2cf-17df-44db-b8cd-dbccf17fb1f6" />

- **RADIUS Server**
  - Copy these settings:  
<img width="550" alt="Screenshot 2025-11-07 102743" src="https://github.com/user-attachments/assets/17e6c6e6-bf18-4e9d-9656-dac470d073b7" />

---

## 🌐 DMZ Server Farm

Similarly, assign static IPs to the DMZ servers:

| Server       | Purpose         |
|---------------|----------------|
| FTP           | File Transfer Protocol |
| EMAIL         | Mail server |
| WEB           | Web hosting |
| NAS-STORAGE   | Network storage |
| APP           | Application server |

Each DMZ device should be assigned its IP manually in the GUI:

- **FTP Server**
  - Copy these settings:  
<img width="550" height="270" alt="Screenshot 2025-11-07 103111" src="https://github.com/user-attachments/assets/81fe1766-7009-48de-a42e-c060772c6756" />

- **EMAIL Server**
  - Copy these settings:  
<img width="550" alt="Screenshot 2025-11-07 103237" src="https://github.com/user-attachments/assets/b92af529-2943-47f2-83c8-7c09635fdf8e" />

- **WEB Server**
  - Copy these settings:  
<img width="550" alt="Screenshot 2025-11-07 103312" src="https://github.com/user-attachments/assets/ff1c3e6c-7b9b-4eda-9e7c-b09fb4575636" />

- **NAS-STORAGE Server**
  - Copy these settings:  
<img width="550" alt="Screenshot 2025-11-07 103424" src="https://github.com/user-attachments/assets/efe19876-8146-42cb-a91d-79bd53d8cb95" />

- **APP Server**
  - Copy these settings:  
<img width="550" alt="Screenshot 2025-11-07 103500" src="https://github.com/user-attachments/assets/22e75343-4d70-4c31-9845-e666e048f839" />

---
