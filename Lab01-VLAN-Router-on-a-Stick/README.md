# Lab 01 — Inter-VLAN Routing (Router-on-a-Stick)

## Overview

This lab demonstrates how to configure VLAN segmentation and enable communication between VLANs using **Router-on-a-Stick**.

Router-on-a-Stick is a common enterprise networking design where a router provides Layer 3 routing for multiple VLANs over a single trunk link.

In this lab we:

* Built a small network in Cisco Packet Tracer
* Created VLANs on a switch
* Assigned switch ports to VLANs
* Configured a trunk link between switch and router
* Created router subinterfaces
* Enabled **inter-VLAN routing**
* Troubleshot connectivity issues

---

# Network Topology

Devices used:

* Cisco 1941 Router
* Cisco 2960 Switch
* 2 PCs
* Cisco Packet Tracer

Topology:

PC0 (VLAN10)
Switch
PC1 (VLAN20)
Router providing VLAN gateways

![Network Topology](Screenshots/01_add_nodes.png)

---

# Step 1 — Connect the Network

All devices were connected using copper straight-through cables.

Router → Switch → PCs

![Device Connections](Screenshots/02_connect.png)

---

# Step 2 — Access Router CLI

Administrative access was enabled on the router.

```
enable
configure terminal
```

![Router CLI Access](Screenshots/03_enable.png)

---

# Step 3 — Configure Router Interface

The router interface connected to the switch was enabled.

```
interface gigabitethernet0/0
no shutdown
```

![Router Interface Configuration](Screenshots/04_assign_ip.png)

---

# Step 4 — Configure PC IP Addresses

Static IP addresses were assigned to both PCs.

### PC0

```
IP Address: 192.168.10.10
Subnet Mask: 255.255.255.0
Gateway: 192.168.10.1
```

### PC1

```
IP Address: 192.168.20.10
Subnet Mask: 255.255.255.0
Gateway: 192.168.20.1
```

![PC IP Configuration](Screenshots/05_desktop_ip_config.png)

---

# Step 5 — Verify Initial Connectivity

Before VLAN segmentation, devices could communicate normally.

![Initial Ping Test](Screenshots/06_ping_connection_check.png)

---

# Step 6 — Create VLANs

Two VLANs were created on the switch.

```
vlan 10
name SALES

vlan 20
name SUPPORT
```

![Create VLANs](Screenshots/07_create_vlan10_vlan20.png)

---

# Step 7 — Assign Switch Ports to VLANs

Switch access ports were assigned to their respective VLANs.

```
interface FastEthernet0/1
switchport mode access
switchport access vlan 10

interface FastEthernet0/2
switchport mode access
switchport access vlan 20
```

![Assign VLAN Ports](Screenshots/08_assign_pc_vlan.png)

---

# Step 8 — VLAN Isolation

After VLAN segmentation, devices in different VLANs could no longer communicate.

This is expected because VLANs isolate traffic at **Layer 2**.

![Ping Failure After VLAN](Screenshots/09_ping_fails_after_vlan.png)

---

# Step 9 — Verify VLAN Configuration

Switch VLAN configuration was verified.

```
show vlan brief
```

![Show VLAN Brief](Screenshots/10_show_vlan_brief.png)

---

# Step 10 — Configure Trunk Port

The switch port connected to the router was converted to a trunk port.

```
interface GigabitEthernet0/1
switchport mode trunk
```

![Switch Trunk Port](Screenshots/12_convert_switch_port_trunk.png)

---

# Step 11 — Configure Router Subinterfaces

Router subinterfaces were created for inter-VLAN routing.

```
interface GigabitEthernet0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface GigabitEthernet0/0.20
encapsulation dot1Q 20
ip address 192.168.20
```
