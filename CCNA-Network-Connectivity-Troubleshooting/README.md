# 🔧 Network Connectivity Troubleshooting

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

[View Topology](screenshots/01.png)

* PC1 → R1 → R2 → R3 → PC2
* Networks:

  * 192.168.1.0/24
  * 192.168.12.0/24
  * 192.168.13.0/24
  * 192.168.3.0/24

---

## 🚨 Problem

Initial ping results showed intermittent connectivity:

[View Initial Ping Failure](screenshots/01.png)

```bash
Reply from 192.168.3.1
Request timed out
Request timed out
Request timed out

Packets: Sent = 4, Received = 1, Lost = 3 (75% loss)
```

---

## 🔍 Investigation & Troubleshooting

---

### 🔹 R1 Misconfiguration

[View R1 Incorrect Route](screenshots/02.png)

```bash
ip route 192.168.3.0 255.255.255.0 192.168.12.3
```

#### ✅ Fix

[View R1 Fix](screenshots/03.png)

```bash
no ip route 192.168.3.0 255.255.255.0 192.168.12.3
ip route 192.168.3.0 255.255.255.0 192.168.12.2
```

#### ✔ Verification

[View R1 Verification](screenshots/04.png)

---

### 🔹 R2 Misconfiguration

[View R2 In]()
