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

![R2 Fix](./06_correct_ip_route.png)

```bash
no ip route 192.168.3.0 255.255.255.0 g0/0
ip route 192.168.3.0 255.255.255.0 192.168.13.3
```

#### ✔ Verification

![R2 Verified](./07_verify_R2_correct_route.png)

---

### 🔹 R3 Misconfiguration

![R3 Issue](./08_missing_static_route_interface_typo.png)

Issues identified:

* Interface misconfiguration
* Missing static route

#### ✅ Fix Interface

![R3 Interface Fix](./09_fix_interface_error.png)

```bash
interface g0/0
ip address 192.168.13.3 255.255.255.0
no shutdown
```

#### ✅ Add Static Route

![R3 Route Fix](./10_add_static_route.png)

```bash
ip route 192.168.1.0 255.255.255.0 192.168.13.2
```

#### ✔ Verification

![R3 Verified](./11_verfy R3_corrections.png)

---

## ✅ Final Verification

![Successful Ping](./12_ping_verifies_connection.png)

```bash
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

✔ Full connectivity restored between PC1 and PC2

---

## 🧠 Key Takeaways

* Incorrect static routes can cause **intermittent packet loss**
* Routers may perform **load balancing across invalid paths**
* Always prefer:

  * ✔ Next-hop IP over exit interface (on Ethernet)
* Use:

  * `show ip route` for validation
* Intermittent ping = 🚩 likely routing issue

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
01_topology_ping_verify_outage.png
02_R1_wrong_hop.png
03_correct_hop_error.png
04_verify_R1_correct_ip_route.png
05_R2_connected_wrong_interface.png
06_correct_ip_route.png
07_verify_R2_correct_route.png
08_missing_static_route_interface_typo.png
09_fix_interface_error.png
10_add_static_route.png
11_verfy R3_corrections.png
12_ping_verifies_connection.png
```

---

## 👨‍💻 Author

Christopher Lee
Aspiring Network Engineer | Cybersecurity Student
