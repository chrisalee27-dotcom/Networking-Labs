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

[View R2 Incorrect Route](screenshots/05.png)

```bash
ip route 192.168.3.0 255.255.255.0 g0/0
```

#### ✅ Fix

[View R2 Fix](screenshots/06.png)

```bash
no ip route 192.168.3.0 255.255.255.0 g0/0
ip route 192.168.3.0 255.255.255.0 192.168.13.3
```

#### ✔ Verification

[View R2 Verification](screenshots/07.png)

---

### 🔹 R3 Misconfiguration

[View R3 Issue](screenshots/08.png)

Issues identified:

* Interface misconfiguration
* Missing static route

#### ✅ Fix Interface

[View R3 Interface Fix](screenshots/09.png)

```bash
interface g0/0
ip address 192.168.13.3 255.255.255.0
no shutdown
```

#### ✅ Add Static Route

[View R3 Route Fix](screenshots/10.png)

```bash
ip route 192.168.1.0 255.255.255.0 192.168.13.2
```

#### ✔ Verification

[View R3 Verification](screenshots/11.png)

---

## ✅ Final Verification

[View Successful Ping](screenshots/12.png)

```bash
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

✔ Full connectivity restored between PC1 and PC2

---

## 🧠 Key Takeaways

* Incorrect static routes can cause **intermittent packet loss**
* Routers may perform **load balancing across invalid paths**
* Always prefer next-hop IP over exit interface
* Use `show ip route` for validation
* Intermittent ping = 🚩 routing issue indicator

---

## 💡 What I Learned

Initially, the issue appeared to be ARP-related due to partial packet success. However, repeated inconsistent ping results revealed a deeper routing issue.

This lab reinforced:

* Structured troubleshooting methodology
* Importance of verifying routing tables
* How routers handle multiple equal-cost paths

---

## 🚀 Skills Demonstrated

* Network troubleshooting
* Static routing configuration
* Cisco IOS CLI
* Routing table analysis
* Problem isolation & resolution

---

## 🛠️ Tools Used

* Cisco Packet Tracer
* Cisco IOS CLI

---

## 📂 Project Structure

```bash
screenshots/
├── 01.png
├── 02.png
├── 03.png
├── 04.png
├── 05.png
├── 06.png
├── 07.png
├── 08.png
├── 09.png
├── 10.png
├── 11.png
└── 12.png
```

---

## 👨‍💻 Author

Christopher Lee
Aspiring Network Engineer | Cybersecurity Student
