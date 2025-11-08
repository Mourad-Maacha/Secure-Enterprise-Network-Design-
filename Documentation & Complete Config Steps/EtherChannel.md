# 🔗 Step 5 — EtherChannel (LACP) Configuration

## 🔍 Explanation

**EtherChannel** (also known as **Link Aggregation**) allows multiple physical links between switches to be bundled into a single **logical channel**, increasing bandwidth and providing redundancy.

In this topology, EtherChannel will be used **only for data transmission between the two Layer 3 switches**.

We’ll be using the **Link Aggregation Control Protocol (LACP)**, which dynamically manages the bundling of links and ensures both ends agree on the channel configuration.

---

## ⚙️ Configuration Details

Both Layer 3 switches are connected using **ports g1/0/9–11**.  
We’ll configure EtherChannel Group 1 using **LACP (active mode)** and then set it as a trunk port.

### 🧱 Configuration Commands

```bash
conf t
int range g1/0/9-11
channel-group 1 mode active
exit

int port-channel 1
switchport mode trunk
do wr
exit
```
> Repeat these steps on both Layer 3 switches.

