# 🔐 Inter-VLAN Routing Lab (ROAS + Trunking)

## 📌 Overview

This lab demonstrates **Inter-VLAN Routing using Router-on-a-Stick (ROAS)** across two switches.

---

## 🖥️ Topology

![Topology](01_Topology.png)

---

## 🧩 VLAN Design

| VLAN    | Network       |
| ------- | ------------- |
| VLAN 10 | 10.0.0.0/26   |
| VLAN 20 | 10.0.0.64/26  |
| VLAN 30 | 10.0.0.128/26 |

---

## ⚙️ Step 1 – Configure Access Ports

### SW1

```bash id="1a2b3c"
interface range f0/1-2
switchport mode access
switchport access vlan 10

interface range f0/3-4
switchport mode access
switchport access vlan 30
```

![SW1 VLAN10](02_create_vlan10_sw1.png)
![SW1 VLAN30](02_create_vlan30_sw1.png)

---

### SW2

```bash id="4d5e6f"
interface range f0/2-3
switchport mode access
switchport access vlan 10

interface f0/1
switchport mode access
switchport access vlan 20
```

![SW2 VLAN10](02_create_vlan10_sw2.png)
![SW2 VLAN20](02_create_vlan20_sw2.png)

---

## 🔗 Step 2 – Configure Trunks

### SW1

```bash id="7g8h9i"
interface g0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30
switchport trunk native vlan 1002
```

![SW1 Trunk](03_sw1_g1_trunk_native_vlan.png)

---

### SW2 (to SW1)

```bash id="10j11k"
interface g0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30
switchport trunk native vlan 1002
```

![SW2 Trunk G1](03_sw2_g1_trunk_native_vlan_vlan30.png)

---

### SW2 (to Router)

```bash id="12l13m"
interface g0/2
switchport mode trunk
switchport trunk allowed vlan 10,20,30
switchport trunk native vlan 1002
```

![SW2 Trunk G2](03_sw2_g2_trunk_native_vlan.png)

---

## 🌐 Step 3 – Router-on-a-Stick

```bash id="14n15o"
interface g0/0
no shutdown

interface g0/0.10
encapsulation dot1q 10
ip address 10.0.0.62 255.255.255.192

interface g0/0.20
encapsulation dot1q 20
ip address 10.0.0.126 255.255.255.192

interface g0/0.30
encapsulation dot1q 30
ip address 10.0.0.190 255.255.255.192
```

![R1 No Shut](04_r1_no_shutdown.png)
![ROAS](05_roas.png)

---

## 🧪 Step 4 – Connectivity Test

```bash id="16p17q"
ping 10.0.0.1
ping 10.0.0.65
ping 10.0.0.129
```

![Ping Test](06_connectivity_test.png)

---

## 🚨 Troubleshooting Lesson

❌ Issue: VLANs could not communicate
✅ Cause: Trunk allowed VLAN mismatch

```bash id="18r19s"
switchport trunk allowed vlan 10,20,30
```

💡 Always ensure trunks match on both sides

---

## 🏁 Result

✔ Full inter-VLAN connectivity achieved
✔ ROAS working correctly
✔ Trunking verified

---

## 🔥 Key Takeaways

* Trunks must match on BOTH sides
* ROAS enables routing with one interface
* VLAN design + trunking = foundation of networking

---

💬 *This lab helped reinforce trunk consistency and real-world troubleshooting skills.*
