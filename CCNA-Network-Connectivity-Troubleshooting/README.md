# 🔧 Network Connectivity Troubleshooting (Static Routing)

### 📡 CCNA Lab | Cisco Packet Tracer

<p align="right">
  <b>🧑‍💻 Christopher Lee</b><br>
  Aspiring Network / Cybersecurity Professional
</p>

---

## 📌 Overview

This lab simulates a real-world troubleshooting scenario where two hosts are unable to communicate due to routing misconfigurations across multiple routers.

The objective was to:

* Diagnose a complete loss of connectivity
* Analyze routing tables using Cisco CLI
* Identify incorrect and missing static routes
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

Initial testing showed **no connectivity** between PC1 and PC2:

[View Initial Ping Failure](screenshots/01.png)

```bash id="n2x4t1"
Request timed out
Request timed out
Request timed out
Request timed out

Packets: Sent = 4, Received = 0, Lost = 4 (100% loss)
```

This indicated:

* Complete communication failure
* Likely routing issue between networks

---

## 🔍 Investigation & Troubleshooting

---

### 🔹 R1 Misconfiguration

[View R1 Incorrect Route](screenshots/02.png)

Incorrect next-hop configured:

```bash id="v5y9k2"
ip route 192.168.3.0 255.255.255.0 192.168.12.3
```

#### ✅ Fix

[View R1 Fix](screenshots/03.png)

```bash id="g7m3q8"
no ip route 192.168.3.0 255.255.255.0 192.168.12.3
ip route 192.168.3.0 255.255.255.0 192.168.12.2
```

#### ✔ Verification

[View R1 Verification](screenshots/04.png)

---

### 🔹 R2 Misconfiguration

[View R2 Incorrect Route](screenshots/05.png)

Incorrect static route using exit interface:

```bash id="c8d1f4"
ip route 192.168.3.0 255.255.255.0 g0/0
```

#### ✅ Fix

[View R2 Fix](screenshots/06.png)

```bash id="u4r6k9"
no ip route 192.168.3.0 255.255.255.0 g0/0
ip route 192.168.3.0 255.255.255.0 192.168.13.3
```

#### ✔ Verification

[View R2 Verification](screenshots/07.png)

---

### 🔹 R3 Misconfiguration

[View R3 Issue](screenshots/08.png)

Issues identified:

* Interface not properly configured
* Missing static route to remote network

#### ✅ Fix Interface

[View R3 Interface Fix](screenshots/09.png)

```bash id="p9w2e6"
interface g0/0
ip address 192.168.13.3 255.255.255.0
no shutdown
```

#### ✅ Add Static Route

[View R3 Route Fix](screenshots/10.png)

```bash id="z3x7c1"
ip route 192.168.1.0 255.255.255.0 192.168.13.2
```

#### ✔ Verification

[View R3 Verification](screenshots/11.png)

---

## 🧩 Root Cause

Multiple routing misconfigurations prevented packets from reaching the destination network:

* Incorrect next-hop on R1
* Improper static route configuration on R2
* Missing route and interface issue on R3

These combined issues resulted in complete loss of connectivity.

---

## ✅ Final Verification

[View Successful Ping](screenshots/12.png)

```bash id="m6n8q2"
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

✔ Full connectivity restored between PC1 and PC2

---

## 🧠 Key Takeaways

* Static routes must use correct next-hop IP addresses
* Exit interfaces can cause issues on multi-access networks
* Always verify routing tables with `show ip route`
* Layered troubleshooting is critical in multi-router environments

---

## 💡 What I Learned

This lab reinforced the importance of a structured troubleshooting approach.

By systematically verifying each router’s configuration and routing table, I was able to isolate and resolve multiple issues contributing to the outage.

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

```bash id="q2k7w9"
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
