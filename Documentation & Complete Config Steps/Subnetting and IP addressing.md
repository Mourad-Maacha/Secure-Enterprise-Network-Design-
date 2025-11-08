# 🌐 Step 6 — Subnetting and IP Addressing

Proper subnetting is the backbone of a secure and scalable network. Below is the complete subnetting plan for the company network, including VLANs, DMZ, Inside Servers, and all point-to-point connections.

---

## 🧭 Company Network

| Category       | Network ID and SM | First and Last Usable Address  | Default Gateway | Broadcast Address |
| -------------- | ----------------- | ------------------------------ | --------------- | ----------------- |
| Management     | 192.168.10.0/24   | 192.168.10.1 – 192.168.10.254  | 192.168.10.1    | 192.168.10.255    |
| WLAN           | 10.20.0.0/16      | 10.20.0.1 – 10.20.255.254      | 10.20.0.1       | 10.20.255.254     |
| LAN            | 172.16.0.0/16     | 172.16.0.1 – 172.16.255.254    | 172.16.0.1      | 172.16.255.255    |
| VoIP           | 172.30.0.0/16     | 172.30.0.1 – 172.30.255.254    | 172.30.0.1      | 172.30.255.255    |
| DMZ            | 10.11.11.0/27     | 10.11.11.1 – 10.11.11.30       | 10.11.11.1      | 10.11.11.31       |
| Inside Servers | 10.11.11.32/27    | 10.11.11.33 – 10.11.11.62      | 10.11.11.33     | 10.11.11.63       |

---

## 🔗 Point-to-Point Connections

| No.             | Network ID       |
| ---------------- | ---------------- |
| CLOUD AREA       | 8.0.0.0/8        |
| ISP1 - INTERNET  | 20.20.20.0/30    |
| ISP2 - INTERNET  | 30.30.30.0/30    |
| ISP1 - FWL1      | 105.100.50.0/30  |
| ISP1 - FWL2      | 105.100.50.4/30  |
| ISP2 - FWL1      | 205.200.100.0/30 |
| ISP2 - FWL2      | 205.200.100.4/30 |
| FWL1 - MLSW1     | 10.2.2.0/30      |
| FWL1 - MLSW2     | 10.2.2.4/30      |
| FWL2 - MLSW1     | 10.2.2.8/30      |
| FWL2 - MLSW2     | 10.2.2.12/30     |

---

## 🧾 Documentation Notes

> Documentation is a crucial part of maintaining a secure and productive network.  
> In Cisco Packet Tracer, label every connection and interface to match the table above.  
> This ensures clarity, accountability, and consistency during configuration and troubleshooting.

<img width="550" alt="Screenshot 2025-11-07 085422" src="https://github.com/user-attachments/assets/473467b5-6881-4326-b87d-5ecf560640a9" />

## 🧠 IP Configuration Process
### 🔹 Layer 3 Switches
1. Enable routing on both Layer 3 switches:
```bash
ip config
ip routing
```
2. Turn ports into Layer 3 interfaces and assign IP addresses:
```bash
int g1/0/1
no switchport
ip address 10.2.2.1 255.255.255.252
no shut

int g1/0/2
no switchport
ip address 10.2.2.5 255.255.255.252
no shut

do wr
```
> Repeat the same configuration on the other Layer 3 switch, adjusting the IPs according to the subnet plan.
### 🔹 Routers
Uncluster the cloud in Cisco Packet Tracer for better visibility, then configure IPs via the GUI for efficiency.

**SEACOM ISP Router Configuration**:
- `g0/0` → Connected to firewall → `105.100.50.1 255.255.255.252`
- `g0/1` → Connected to second firewall → `105.100.50.5 255.255.255.252`
- `g0/2` → Connected to Internet → `20.20.20.1 255.255.255.252`

Repeat similar IP assignments for all remaining ISP routers.

<img width="550" alt="Screenshot 2025-11-07 091057" src="https://github.com/user-attachments/assets/cc8b01aa-1058-4e44-8abc-7ffd07460a93" />

### 🔹 USA and Algeria Computers
Use the GUI to quickly assign static IP addresses for the test PCs.

| Location | IP Address | Subnet Mask | Default Gateway |
| -------- | ---------- | ----------- | --------------- |
| USA      | 8.0.0.10   | 255.0.0.0   | 8.0.0.1         |
| ALGERIA  | 8.0.0.20   | 255.0.0.0   | 8.0.0.1         |

<img width="550" alt="Screenshot 2025-11-07 102129" src="https://github.com/user-attachments/assets/f4c1c844-cc85-4f3a-acc3-beba105eaf73" />
<img width="550" alt="Screenshot 2025-11-07 102111" src="https://github.com/user-attachments/assets/1880d242-1b4f-48c6-a2b5-e30637db4bd4" />

