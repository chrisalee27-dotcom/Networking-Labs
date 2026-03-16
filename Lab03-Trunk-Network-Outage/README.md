# Lab 03 — Trunk Network Outage

<div align="right">

| Lab Info | |
|---|---|
| Lab | 03 |
| Topic | Trunk Failure Troubleshooting |
| Tool | Cisco Packet Tracer |
| Focus | Network Outage Investigation |
| Author | Christopher Lee |

</div>

---

## Overview

This lab simulates a **network outage caused by a trunk port misconfiguration** between a switch and router.

In a VLAN environment, trunk ports are required to allow multiple VLANs to traverse a single physical link. If a trunk port is accidentally changed to an access port, VLAN traffic cannot reach the router, resulting in **loss of connectivity for devices on those VLANs**.

In this scenario, the network is first configured correctly and verified. A trunk misconfiguration is then introduced to simulate a network outage. The issue is investigated using standard switch diagnostic commands and the trunk configuration is restored.

---

## Lab Topology

Devices used:

- Cisco 1941 Router  
- Cisco 2960 Switch  
- 2 PCs  

Network layout:

```
Router
   |
Switch
 /     \
PC0   PC1
```

Topology screenshot:

➡️ [View Topology](Screenshots/01_lab_toplolgy.png)

---

## Step 1 — Configure VLANs

Two VLANs were created on the switch.

- VLAN 10 — SALES  
- VLAN 20 — SUPPORT  

Screenshot:

➡️ [View VLAN Configuration](Screenshots/02_configure_network.png)

---

## Step 2 — Configure Switch Access Ports

Switch ports were configured as access ports and assigned to VLANs.

| Device | Switch Port | VLAN |
|------|------|------|
| PC0 | Fa0/1 | VLAN 10 |
| PC1 | Fa0/2 | VLAN 20 |

Screenshot:

➡️ [View Switch Port Assignment](Screenshots/03_configure_switchports.png)

---

## Step 3 — Configure Trunk Link

The switch uplink connected to the router was configured as a trunk port to allow traffic from multiple VLANs.

```
interface gigabitEthernet0/1
switchport mode trunk
```

Screenshot:

➡️ [View Trunk Configuration](Screenshots/04_configure_trunk.png)

---

## Step 4 — Configure Router Subinterfaces

Router-on-a-Stick routing was implemented using router subinterfaces.

```
interface g0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface g0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
```

Screenshot:

➡️ [View Router Configuration](Screenshots/05_router_config.png)

---

## Step 5 — Configure PC IP Addresses

The PCs were configured with static IP addresses.

PC0

```
IP Address: 192.168.10.10
Gateway: 192.168.10.1
```

PC1

```
IP Address: 192.168.20.10
Gateway: 192.168.20.1
```

Screenshot:

➡️ [View PC Configuration](Screenshots/06_pc_ip_config.png)

---

## Step 6 — Verify Network Connectivity

Connectivity was verified before introducing the outage.

Ping from PC0 to its default gateway succeeded.

Screenshot:

➡️ [View Connectivity Verification](Screenshots/07_ping_network_verification.png)

---

## Step 7 — Simulate Network Outage

To simulate a real troubleshooting scenario, the trunk link was intentionally misconfigured.

```
interface gigabitEthernet0/1
switchport mode access
```

This removed trunk functionality and prevented VLAN traffic from reaching the router.

Screenshot:

➡️ [View Outage Simulation](Screenshots/08_outage_simulated.png)

---

## Step 8 — Verify Connectivity Failure

After the trunk configuration was removed, connectivity tests failed.

Ping to the gateway from PC0 no longer worked.

Screenshot:

➡️ [View Ping Failure](Screenshots/09_ping_outage_verified.png)

---

## Step 9 — Investigate the Issue

The switch was inspected using diagnostic commands.

```
show interfaces trunk
```

The command returned **no active trunk ports**, confirming that the switch uplink was no longer trunking.

Screenshot:

➡️ [View Trunk Status](Screenshots/10_no_trunk.png)

Switch configuration was reviewed to identify the root cause.

Screenshot:

➡️ [View Switch Configuration](Screenshots/11_switch_config.png)

---

## Step 10 — Restore Trunk Configuration

The trunk configuration was restored.

```
interface gigabitEthernet0/1
switchport mode trunk
```

Screenshot:

➡️ [View Correct Trunk Configuration](Screenshots/12_show_correct_interfaces.png)

---

## Step 11 — Verify Network Restoration

Connectivity tests confirmed the network was restored.

Ping to the gateway from PC0 succeeded again.

Screenshot:

➡️ [View Restored Connectivity](Screenshots/13_ping_network_verification_restored.png)

---

## Troubleshooting Commands Used

```
show interfaces trunk
show running-config
show vlan brief
ping
```

These commands are commonly used by **Network Operations Center (NOC) engineers** to diagnose Layer 2 connectivity problems.

---

## Skills Demonstrated

- VLAN configuration  
- Switch port assignment  
- Trunk configuration  
- Router-on-a-Stick routing  
- Network outage investigation  
- CLI troubleshooting  
- Connectivity verification  

---

## Key Takeaway

A misconfigured trunk port can prevent VLAN traffic from reaching the router, resulting in widespread connectivity failures.

Understanding how to verify trunk status and inspect switch configurations is critical when troubleshooting Layer 2 network outages.

---
