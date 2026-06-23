# Cisco Campus Network Lab

## Overview

This project demonstrates the implementation of a small enterprise-style Cisco campus network using a Cisco 1841 router and two Cisco Catalyst 3560 switches.

The lab was built to gain practical experience with core CCNA networking concepts including VLAN segmentation, Router-on-a-Stick (ROAS), DHCP services, trunking, EtherChannel, Spanning Tree Protocol (STP), and remote device management.

The topology follows a simplified Access–Distribution design, where SW1 acts as the distribution switch and SW2 serves as the access switch.

---

## Network Topology

```text
                    R1 (Cisco 1841)
                          |
                     802.1Q Trunk
                          |
                     SW1 (3560)
                 Distribution Layer
                          |
                ===================
                ||   EtherChannel  ||
                ===================
                  Fa0/10   Fa0/12
                          |
                     SW2 (3560)
                    Access Layer
                     /        \
                    /          \
                 PC1            PC2
```

---

## Hardware

| Device      | Model               |
| ----------- | ------------------- |
| Router      | Cisco 1841          |
| Switch      | Cisco Catalyst 3560 |
| Switch      | Cisco Catalyst 3560 |
| End Devices | 2 PCs/Laptops       |

---

## Technologies Implemented

### VLAN Segmentation

Four VLANs were created to separate network traffic and improve management.

| VLAN | Name   | Purpose            |
| ---- | ------ | ------------------ |
| 10   | USERS  | User devices       |
| 20   | STAFF  | Staff devices      |
| 30   | MGMT   | Management network |
| 99   | NATIVE | Native VLAN        |

---

### Router-on-a-Stick (ROAS)

Inter-VLAN routing is provided by the Cisco 1841 router using 802.1Q subinterfaces.

Configured subinterfaces:

* Fa0/0.10
* Fa0/0.20
* Fa0/0.30
* Fa0/0.99 (Native VLAN)

This allows devices in different VLANs to communicate through the router.

---

### DHCP Services

The router provides DHCP services for client VLANs.

Configured DHCP pools:

* VLAN 10
* VLAN 20

Each pool distributes:

* IP Address
* Subnet Mask
* Default Gateway
* DNS Server

---

### Trunking

802.1Q trunks were configured between:

* R1 ↔ SW1
* SW1 ↔ SW2

Allowed VLANs:

```text
10,20,30,99
```

Native VLAN:

```text
99
```

---

### EtherChannel (LACP)

An EtherChannel bundle was configured between SW1 and SW2 using LACP.

Member Interfaces:

```text
Fa0/10
Fa0/12
```

Benefits:

* Increased bandwidth
* Redundancy
* Load balancing

Verification:

```cisco
show etherchannel summary
```

---

### Spanning Tree Protocol (STP)

SW1 was configured as the root bridge for VLANs:

* VLAN 10
* VLAN 20
* VLAN 30

This ensures predictable Layer 2 forwarding paths and prevents switching loops.

---

### Remote Management

Remote administration was configured using:

* Telnet
* Local user database
* Privileged EXEC access

Management VLAN:

```text
192.168.30.0/24
```

Management IP Addresses:

| Device | Address       |
| ------ | ------------- |
| R1     | 192.168.30.1  |
| SW1    | 192.168.30.11 |
| SW2    | 192.168.30.12 |

---

## IP Addressing Scheme

| VLAN    | Network         | Gateway      |
| ------- | --------------- | ------------ |
| VLAN 10 | 192.168.10.0/24 | 192.168.10.1 |
| VLAN 20 | 192.168.20.0/24 | 192.168.20.1 |
| VLAN 30 | 192.168.30.0/24 | 192.168.30.1 |

---

## Verification Commands

### VLANs

```cisco
show vlan brief
```

### Trunking

```cisco
show interfaces trunk
```

### EtherChannel

```cisco
show etherchannel summary
```

### STP

```cisco
show spanning-tree
```

### DHCP

```cisco
show ip dhcp binding
```

### Interface Status

```cisco
show ip interface brief
```

---

## Troubleshooting Performed

During implementation, several real-world networking issues were encountered and resolved:

* Native VLAN mismatches
* EtherChannel compatibility errors
* Trunk configuration issues
* VLAN forwarding problems
* SVI status troubleshooting
* Inter-VLAN routing verification
* Telnet authentication configuration


