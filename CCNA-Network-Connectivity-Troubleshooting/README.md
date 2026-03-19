# 🔧 Intermittent Network Connectivity Troubleshooting

### 📡 Static Routing Lab | Cisco Packet Tracer

<p align="right">
  <b>🧑‍💻 Christopher Lee</b><br>
  Aspiring Network / Cybersecurity Professional
</p>

---

## 📌 Overview

This lab simulates a real-world troubleshooting scenario where two hosts are unable to communicate due to multiple routing misconfigurations across routers.

The objective was to:

* Diagnose intermittent connectivity issues
* Analyze routing tables using Cisco CLI
* Identify incorrect static routes
* Restore full end-to-end connectivity

---

## 🖥️ Network Topology

![Topology](./01_topology_ping_verify_outage.png)

* PC1 → R1 → R2 → R3 → PC2
* Networks:

  * 192.168.1.0/24
  * 192.168.12.0/24
  * 192.168.13.0/24
  * 192.168.3.0/24

---

## 🚨 Problem

Initial ping results showed intermittent connectivity:

![Initial Ping Failure](./01_topology_ping_verify_outage.png)

```bash
Reply from 192.168.3.1
Request timed out
Request timed out
Request timed out

Packets: Sent = 4, Received = 1, Lost = 3 (75% loss)
```

This indicated:

* Partial connectivity
* Possible routing inconsistency

---

## 🔍 Investigation & Troubleshooting

---

### 🔹 R1 Misconfiguration

![R1 Incorrect Route](./02_R1_wrong_hop.png)

Incorrect next-hop configured:

```bash
ip route 192.168.3.0 255.255.255.0 192.168.12.3
```

#### ✅ Fix

![R1 Fix](./03_correct_hop_error.png)

```bash
no ip route 192.168.3.0 255.255.255.0 192.168.12.3
ip route 192.168.3.0 255.255.255.0 192.168.12.2
```

#### ✔ Verification

![R1 Verified](./04_verify_R1_correct_ip_route.png)

---

### 🔹 R2 Misconfiguration

![R2 Incorrect Route](./05_R2_connected_wrong_interface.png)

Used exit interface instead of next-hop:

```bash
ip route 192.168.3.0 255.255.255.0 g0/0
```

#### ✅ Fix

![R2 Fix]()
