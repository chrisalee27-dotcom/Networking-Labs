# 🔐 Inter-VLAN Routing Lab (ROAS + Trunking)

## 📌 Overview

This lab demonstrates **Inter-VLAN Routing using Router-on-a-Stick (ROAS)** across two switches.

---

## 🖥️ Topology

![Topology](screenshots/01_Topology.png)

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

```bash id="a1b2c3"
interface range f0/1-2
switchport mode access
switchport access vlan 10

interface range f0/3-4
switchport mode access
switchport access vlan 30
```

![SW1 VLAN10](screenshots/02_create_vlan10_sw1.png)
![SW1 VLAN30](screenshots/02_create_vlan30_sw1.png)

---

### SW2

```bash id="d4e5f6"
interface range f0/2-3
switchport mode access
switchport access vlan 10

interface f0/1
switchport mode access
switchport access vlan 20
```

![SW2 VLAN10](screenshots/02_create_vlan10_sw2.png)
![SW2 VLAN20](screenshots/02_create_vlan20_sw2.png)

---

## 🔗 Step 2 – Configure Trunks

### SW1

```bash id="g7h8i9"
interface g0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30
switchport trunk native vlan 1002
```

![SW1 Trunk](screenshots/03_sw1_g1_trunk_native_vlan.png)

---

### SW2 (to SW1)

```bash id="j10k11"
interface g0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30
switchport trunk native vlan 1002
```

![SW2 Trunk G1](screenshots/03_sw2_g1_trunk_native_vlan_vlan30.png)

---

### SW2 (to Router)

```bash id="l12m13"
interface g0/2
switchport mode trunk
switchport trunk allowed vlan 10,20,30
switchport trunk native vlan 1002
```

![SW2 T]()
