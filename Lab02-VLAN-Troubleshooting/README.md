# Lab 02 — VLAN Troubleshooting

<div align="right">

| Lab Info | |
|---|---|
| Lab | 02 |
| Topic | VLAN Troubleshooting |
| Tool | Cisco Packet Tracer |
| Focus | Network Diagnostics |
| Author | Christopher Lee |

</div>

---

## Overview

This lab simulates a **Network Operations Center (NOC) troubleshooting scenario** where a user reports that their device cannot access the network.

The objective is to:

- Investigate the connectivity issue
- Identify the root cause
- Correct the misconfiguration
- Restore network communication

The issue in this scenario is caused by a **VLAN misconfiguration on a switch port**.

---

## Lab Topology

Devices used:

- Cisco 1941 Router
- Cisco 2960 Switch
- 2 PCs

Network structure:

```
Router
   |
Switch
 /     \
PC0   PC1
```

Topology screenshot:

➡️ [View Topology](Screenshots/01_lab_topology.png)

---

## Step 1 — Create VLANs

Two VLANs were created on the switch.

- VLAN 10 — SALES  
- VLAN 20 — SUPPORT

Screenshot:

➡️ [View VLAN Creation](Screenshots/02_vlan_creation.png)

---

## Step 2 — Assign Switch Ports

Ports were configured as access ports and assigned to VLANs.

- PC0 → VLAN 10  
- PC1 → VLAN 20

Screenshot:

➡️ [View VLAN Assignment](Screenshots/03_vlan_assignment.png)

---

## Step 3 — Configure Trunk Link

The switch port connected to the router was configured as a trunk port to allow multiple VLANs to traverse the link.

Screenshot:

➡️ [View Trunk Configuration](Screenshots/04_trunk_port.png)

---

## Step 4 — Configure Router Subinterfaces

Router-on-a-Stick routing was implemented using subinterfaces.

```
interface g0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface g0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
```

Screenshot:

➡️ [View Router Subinterfaces](Screenshots/05_router_subinterface.png)

---

## Step 5 — Introduce the Problem

To simulate a real troubleshooting scenario, the network was intentionally misconfigured.

PC0 was moved to the **wrong VLAN**.

```
interface fa0/1
switchport access vlan 20
```

This caused the device to lose connectivity with its gateway.

Screenshot:

➡️ [View Network Misconfiguration](Screenshots/06_break_network.png)

---

## Step 6 — Identify the Issue

Connectivity testing revealed the failure.

Ping test from PC0 to its gateway failed.

Screenshot:

➡️ [View Ping Failure](Screenshots/07_ping_fails.png)

Switch diagnostics were used to inspect VLAN assignments.

```
show vlan brief
```

Screenshot:

➡️ [View VLAN Verification](Screenshots/08_vlan_brief.png)

The investigation revealed that **PC0 was assigned to the incorrect VLAN**.

---

## Step 7 — Correct the VLAN Assignment

The switch port was reconfigured to place PC0 back into VLAN 10.

```
interface fa0/1
switchport access vlan 10
```

Screenshot:

➡️ [View VLAN Fix](Screenshots/09_vlan_fixed.png)

---

## Step 8 — Verify Connectivity

After correcting the configuration, connectivity was restored.

Ping testing confirmed that the device could again reach the default gateway.

Screenshot:

➡️ [View Ping Success](Screenshots/10_ping_restored.png)

---

## Troubleshooting Commands Used

```
show vlan brief
show running-config
ping
```

These commands are commonly used by **Network Operations Center (NOC) engineers** to diagnose VLAN connectivity problems.

---

## Skills Demonstrated

- VLAN configuration
- Switch port assignment
- Router-on-a-Stick configuration
- Network troubleshooting
- CLI diagnostics
- Connectivity verification

---

## Key Takeaway

A simple **VLAN misconfiguration can prevent devices from reaching their gateway and disrupt network connectivity**.

Proper troubleshooting methodology — including verification commands and connectivity testing — is essential for identifying and resolving these issues.

---

