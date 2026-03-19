# Intermittent Network Connectivity Troubleshooting
### Static Routing Lab | Cisco Packet Tracer

<p align="right">
  <b>Christopher Lee</b><br>
  Aspiring Network / Cybersecurity Professional
</p>

---

## Overview
This lab simulates a troubleshooting scenario where two hosts were unable to communicate because of multiple static routing misconfigurations across three routers.

The objective was to:
- diagnose intermittent connectivity
- analyze routing tables
- identify incorrect static routes
- correct misconfigurations
- restore end-to-end connectivity

---

## Network Topology

[Network Topology](01_topology_ping_verify_outage.png)

- PC1 -> R1 -> R2 -> R3 -> PC2
- Networks used:
  - 192.168.1.0/24
  - 192.168.12.0/24
  - 192.168.13.0/24
  - 192.168.3.0/24

---

## Problem

Initial testing from PC1 to PC2 showed intermittent packet loss.

[Initial Connectivity Failure](01_topology_ping_verify_outage.png)

Example result:

```bash
Reply from 192.168.3.1
Request timed out
Request timed out
Request timed out

Packets: Sent = 4, Received = 1, Lost = 3 (75% loss)
