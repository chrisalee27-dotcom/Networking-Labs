# Lab 01 – Inter-VLAN Routing (Router-on-a-Stick)

## Overview

This lab demonstrates how to configure VLAN segmentation and enable communication between VLANs using **Router-on-a-Stick**.

Router-on-a-Stick is a common enterprise networking design where a router performs Layer 3 routing for multiple VLANs over a single trunk connection.

The goal of this lab was to:

* Create VLANs
* Assign switch ports to VLANs
* Configure trunking between the switch and router
* Configure router subinterfaces
* Enable inter-VLAN communication
* Troubleshoot connectivity issues

---

## Network Topology

The lab environment consists of:

* Cisco 1941 Router
* Cisco 2960 Switch
* 2 PCs
* Cisco Packet Tracer

Network layout:

```
PC0 (VLAN10) ----\
                   \
                    Switch ---- Router
                   /
PC1 (VLAN20) ----/
```

Screenshot:

![Topology](01_add_nodes.png)

---

# Step 1 – Build Network and Connect Devices

Devices were added to the topology and connected using copper straight-through cables.

Router → Switch → PCs

Screenshot:

![Connections](02_connect.png)

---

# Step 2 – Access Router CLI

The router CLI was accessed and administrative mode enabled.

```
enable
configure terminal
```

Screenshot:

![Enable Mode](03_enable.png)

---

# Step 3 – Configure Router Interface

The router interface connected to the switch was configured and enabled.

```
interface gigabitethernet0/0
no shutdown
```

Screenshot:

![Assign Router IP](04_assign_ip.png)

---

# Step 4 – Configure PC IP Addresses

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

Screenshot:

![PC IP Configuration](05_desktop_ip_config.png)

---

# Step 5 – Initial Connectivity Test

Before VLAN configuration, devices could communicate normally.

Screenshot:

![Ping Test](06_ping_connection_check.png)

---

# Step 6 – Create VLANs

Two VLANs were created on the switch.

```
vlan 10
name SALES

vlan 20
name SUPPORT
```

Screenshot:

![Create VLANs](07_create_vlan10_vlan20.png)

---

# Step 7 – Assign Switch Ports to VLANs

Switch access ports were assigned to their respective VLANs.

```
interface FastEthernet0/1
switchport mode access
switchport access vlan 10

interface FastEthernet0/2
switchport mode access
switchport access vlan 20
```

Screenshot:

![Assign VLAN Ports](08_assign_pc_vlan.png)

---

# Step 8 – Connectivity Failure After VLAN Segmentation

After VLAN segmentation was implemented, devices in different VLANs could no longer communicate.

This is expected behavior because VLANs isolate Layer 2 networks.

Screenshot:

![Ping Failure](09_ping_fails_after_vlan.png)

---

# Step 9 – Verify VLAN Configuration

The switch VLAN table was verified.

```
show vlan brief
```

Screenshot:

![Show VLAN Brief](10_show_vlan_brief.png)

---

# Step 10 – Verify Switch Configuration

Switch interface configuration was confirmed.

```
show running-config
```

Screenshot:

![Show Running Config](11_show_running_config.png)

---

# Step 11 – Configure Trunk Port

The switch port connected to the router was converted to a trunk port.

```
interface GigabitEthernet0/1
switchport mode trunk
```

Screenshot:

![Trunk Port](12_convert_switch_port_trunk.png)

---

# Step 12 – Configure Router Subinterfaces

Router subinterfaces were created to support inter-VLAN routing.

```
interface GigabitEthernet0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface GigabitEthernet0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
```

Screenshot:

![Router Subinterfaces](13_configure_router_subinterface.png)

---

# Step 13 – Update PC Gateways

PC gateway addresses were updated to use the router subinterfaces.

Screenshot:

![Update PC Gateway](14_update_pc_ip.png)

---

# Step 14 – Troubleshooting Connectivity Issues

During the configuration process, connectivity issues were investigated and resolved.

Troubleshooting steps included:

* Verifying router interface status
* Confirming trunk configuration
* Checking VLAN assignments
* Removing incorrect router IP configuration
* Re-verifying router subinterfaces

Screenshots:

![Troubleshooting](16_isolate_router_setup_problem.png)

![Router Verification](18_verify_proper_router_config.png)

---

# Step 15 – Final Verification

Inter-VLAN routing was successfully established.

PC0 (VLAN10) can now communicate with PC1 (VLAN20).

Screenshot:

![Inter VLAN Routing Confirmed](22_inter_vlan_routing_confirmed.png)

---

# Key Networking Concepts Demonstrated

This lab covers several important networking fundamentals:

* VLAN segmentation
* Access ports
* Trunk ports
* 802.1Q tagging
* Router-on-a-Stick architecture
* Inter-VLAN routing
* Network troubleshooting methodology

---

# Commands Used

Switch Commands

```
show vlan brief
show running-config
show interfaces trunk
```

Router Commands

```
show ip interface brief
show running-config
```

---

# Skills Demonstrated

* VLAN configuration
* Layer 2 switching
* Inter-VLAN routing
* Router subinterfaces
* Network troubleshooting
* Packet Tracer network simulation

---

# Conclusion

This lab demonstrates how VLAN segmentation can isolate network traffic and how **Router-on-a-Stick inter-VLAN routing** enables communication between VLANs.

The troubleshooting process reinforced the importance of verifying trunk configuration, router interfaces, and VLAN assignments when diagnosing connectivity issues in enterprise networks.
