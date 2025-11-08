# ☎️ Step 16 — VoIP Configurations

In this final step, we’ll configure the **Cisco Voice Gateway**, enable **DHCP** for VoIP devices, and set up **telephony service** so all IP phones can communicate across departments.

---

### 🧩 1. Configure the Voice Gateway Interface

Let’s begin by bringing up the outside port and creating a **subinterface for VLAN 70**.

```bash
conf t
int f0/0
no shut
exit
int f0/0.70
encapsulation dot1q 70
ip address 172.30.0.1 255.255.0.0
exit
```

Now create a DHCP pool for VLAN 70:

```bash
conf t
ip dhcp pool VOIP-POOL
network 172.30.0.0 255.255.0.0
default-router 172.30.0.1
option 150 ip 172.30.0.1
exit

do wr
```

### 📞 2. Enable Telephony Service

Next, we’ll enable telephony-service and configure 10 directory numbers (DNs) for the phones.

```bash
conf t
telephony-service
max-ephones 30
max-dn 30
ip source-address 172.30.0.1 port 2000
auto assign 1 to 30
exit

ephone-dn 1
number 401
exit
ephone-dn 2
number 402
exit
ephone-dn 3
number 403
exit
ephone-dn 4
number 404
exit
ephone-dn 5
number 405
exit
ephone-dn 6
number 406
exit
ephone-dn 7
number 407
exit
ephone-dn 8
number 408
exit
ephone-dn 9
number 409
exit
ephone-dn 10
number 4010
exit

do wr
```

### 📟 3. Verify IP Phones

Once configured, hover over the phones in your topology.
You should see that each has received an IP address and has been assigned a Line Number.

<img width="550" alt="Pasted image 20251107150417" src="https://github.com/user-attachments/assets/711e905a-e3f5-4371-b5c5-97c77fd34ee0" />

#$$ 📲  4 — Test VoIP Calls

Let’s test the setup by making a call between two departments.

---

### 1. Open the Phones

Click the **Marketing Department** phone, then open the **GUI interface**.

<img width="550" alt="Pasted image 20251107150702" src="https://github.com/user-attachments/assets/f3ab6c41-1109-4a26-b1ab-79d81d380727" />

- **Marketing Department → Line 4010**  
- **ICT Department → Line 405**

---

### 2. Make the Call

Use the on-screen keypad to call **405**.

<img width="550" alt="Pasted image 20251107150846" src="https://github.com/user-attachments/assets/3d611f4a-37aa-4942-8c8c-1420d0a1af39" />

✅ The phone should **ring** — VoIP is working perfectly!

---

# 🎉 Lab Complete!

You’ve successfully configured and verified all major network services.

---

**This concludes the entire lab.**  
👏 Excellent job completing the full enterprise network configuration!
