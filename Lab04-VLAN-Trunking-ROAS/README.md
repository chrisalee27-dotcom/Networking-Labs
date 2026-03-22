# 🔐 Inter-VLAN Routing Lab (ROAS + Trunking)

## 📌 Overview

This lab demonstrates **Inter-VLAN Routing using Router-on-a-Stick (ROAS)** across two switches.
The goal is to configure VLAN segmentation, trunk links, and router subinterfaces so that all hosts across different VLANs can communicate.

---

## 🧠 Objectives

* Configure VLANs across multiple switches
* Assign access ports to correct VLANs
* Configure trunk links between switches
* Implement Router-on-a-Stick (ROAS)
* Verify end-to-end connectivity

---

## 🖥️ Topology

![Topology](01_Topology.png)

---

## 🧩 VLAN & Subnet Design

| VLAN    | Network       | Devices            |
| ------- | ------------- | ------------------ |
| VLAN 10 | 10.0.0.0/26   | PC1, PC2, PC6, PC7 |
| VLAN 20 | 10.0.0.64/26  | PC5                |
| VLAN 30 | 10.0.0.128/26 | PC3, PC4           |

---

## ⚙️ Step 1 – Configure Access Ports

### SW1

```bash
interface range f0/1-2
switchport mode access
switchport access vlan 10

interface range f0/3-4
switchport mode access
switchport access vlan 30
```

📸
![SW1 VLAN10](02_create_vlan10_sw1.png)
![SW1 VLAN30](02_create_vlan30_sw1.png)

---

### SW2

```bash
interface range f0/2-3
switchport mode access
switchport access vlan 10

interface f0/1
switchport mode access
switchport access vlan 20
```

📸
![SW2 VLAN10](02_create_vlan10_sw2.png)
![SW2 VLAN20](02_create_vlan20_sw2.png)

---

## 🔗 Step 2 – Configure Trunks

### SW1 → SW2

```bash
interface g0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30
switchport trunk native vlan 1002
```

📸
![SW1 Trunk](03_sw1_g1_trunk_native_vlan.png)

---

### SW2 → SW1

```bash
interface g0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30
switchport trunk native vlan 1002
```

📸
![SW2 Trunk G1](03_sw2_g1_trunk_native_vlan_vlan 30.png)

---

### SW2 → R1

```bash
interface g0/2
switchport mode trunk
switchport trunk allowed vlan 10,20,30
switchport trunk native vlan 1002
```

📸
![SW2 Trunk G2](03_sw2_g2_trunk_native_vlan_.png)

---

## 🌐 Step 3 – Configure Router-on-a-Stick

### Enable Interface

```bash
interface g0/0
no shutdown
```

📸
![R1 No Shut](04_r1_no_shutdown.png)

---

### Subinterfaces

```bash
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

📸
![ROAS Config](05_roas.png)

---

## 🧪 Step 4 – Connectivity Test

```bash
ping 10.0.0.1
ping 10.0.0.65
ping 10.0.0.129
```

📸
![Ping Test](06_connectivity_test.png)

---

## 🚨 Troubleshooting Insight (Key Lesson)

During the lab, connectivity initially failed due to:

👉 **Trunk allowed VLAN mismatch between switches**

