# Cisco Campus Network Lab

## Overview

This project demonstrates the implementation of a small enterprise-style Cisco campus network using a Cisco 1841 router and two Cisco Catalyst 3560 switches.

The lab was built to gain practical hands-on experience with core CCNA/CCNP-level networking concepts including VLAN segmentation, Router-on-a-Stick (ROAS), DHCP services, NAT overload, trunking, EtherChannel, Spanning Tree Protocol (STP), port-security, and remote device management.

The topology follows a simplified **Access–Distribution design**, where:
- SW1 acts as the Distribution switch
- SW2 acts as the Access switch
- R1 provides Layer 3 routing + Internet NAT via ISP (BT WiFi router)

---

## Network Topology
                BT WiFi (ISP / Internet)
                           |
                R1 (Cisco 1841 Router)
                 Inter-VLAN Routing + NAT
                           |
                    802.1Q Trunk Link
                           |
                      SW1 (3560)
                 Distribution Layer
                           |
                ======================
                ||  EtherChannel    ||
                ======================
                  Fa0/10    Fa0/12
                           |
                      SW2 (3560)
                    Access Layer
              /       |        |       \
          VLAN10   VLAN20   VLAN40    VLAN50
          USERS     STAFF    MEDIA     VOICE

---

## Hardware

| Device      | Model               |
| ----------- | ------------------- |
| Router      | Cisco 1841          |
| Switch      | Cisco Catalyst 3560 |
| Switch      | Cisco Catalyst 3560 |
| End Devices | PCs / Laptops / Phones / TVs |

---

## Technologies Implemented

## VLAN Segmentation

| VLAN | Name   | Purpose            |
|------|--------|--------------------|
| 10   | USERS  | User devices       |
| 20   | STAFF  | Staff devices      |
| 30   | MGMT   | Network management |
| 40   | MEDIA  | TVs / streaming    |
| 50   | VOICE  | IP phones          |
| 99   | NATIVE | Trunk native VLAN  |

---

## Router-on-a-Stick (ROAS)

Inter-VLAN routing is performed on the Cisco 1841 router using 802.1Q subinterfaces:

- Fa0/0.10 - VLAN 10
- Fa0/0.20 - VLAN 20
- Fa0/0.30 - VLAN 30
- Fa0/0.40 - VLAN 40
- Fa0/0.50 - VLAN 50
- Fa0/0.99 - Native VLAN

---

## DHCP Services

The router provides DHCP for all VLANs.

Each DHCP pool provides:
- IP address
- Subnet mask
- Default gateway
- DNS servers (8.8.8.8 / 1.1.1.1)

Excluded addresses:
- Gateway IPs (.1–.20 range)

---

## NAT (Internet Access)

Internet access is provided via BT WiFi router.

### NAT Configuration

- PAT (Port Address Translation) enabled
- Inside VLANs translated to WAN interface IP

### Result

- Internal devices access the internet successfully
- Verified via ping to 8.8.8.8

---

## Trunking

Trunk links exist between:

- R1 - SW1
- SW1 - SW2

Allowed VLANs:
10,20,30,40,50,99

Native VLAN:
99


---

## EtherChannel (LACP)

Configured between SW1 and SW2:

- Fa0/10
- Fa0/12

Benefits:
- Increased bandwidth
- Redundancy
- Load balancing

---

## Spanning Tree Protocol (STP)

- SW1 is the root bridge for VLANs 10, 20, 30
- PortFast enabled on access ports
- BPDU Guard enabled for edge protection

---

## Port Security (SW2)

- Sticky MAC learning enabled
- Max MAC per port: 1 (some ports adjusted to 2)
- Violation mode: shutdown
- Errdisable recovery enabled

### Issue Encountered
- MAC address movement triggered psecure-violation
- Caused interface err-disable state

### Resolution
- Cleared sticky MAC entries
- Reset interfaces (shutdown / no shutdown)
- Adjusted port-security settings

---

## Voice & Media VLANs

- VLAN 40 - Media devices (TVs/streaming)
- VLAN 50 → Voice devices (IP phones)

---

## Power over Ethernet (PoE)

PoE functionality was considered for the Voice VLAN (VLAN 50) to support powered end devices such as IP phones and wireless access points.

PoE-enabled ports were planned for:
Fa0/14
Fa0/16
Fa0/18

These ports are configured for voice devices such as IP phones.


## Remote Management

- Telnet enabled (lab use only)
- Local user authentication
- Privilege level 15 admin account

---

## Management Network

| Device | IP Address      |
|--------|----------------|
| R1     | 192.168.30.1   |
| SW1    | 192.168.30.11  |
| SW2    | 192.168.30.12  |

---

## IP Addressing Scheme

| VLAN | Network         | Gateway        |
|------|----------------|----------------|
| 10   | 192.168.10.0/24 | 192.168.10.1   |
| 20   | 192.168.20.0/24 | 192.168.20.1   |
| 30   | 192.168.30.0/24 | 192.168.30.1   |
| 40   | 192.168.40.0/24 | 192.168.40.1   |
| 50   | 192.168.50.0/24 | 192.168.50.1   |

---

## Verification Commands

```cisco
show vlan brief
show interfaces trunk
show etherchannel summary
show spanning-tree
show ip dhcp binding
show ip interface brief
show ip nat translations
show ip nat statistics
```
