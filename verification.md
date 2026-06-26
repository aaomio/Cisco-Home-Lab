# Network Verification

## Overview

This document provides verification outputs and proof of functionality for the Cisco Campus Network Lab.  
All core services including VLAN segmentation, trunking, EtherChannel, DHCP, NAT, STP, and port-security have been tested and confirmed working.

---

## VLAN Verification

### Command
```cisco
show vlan brief
```

### Results
- VLANs 10, 20, 30, 40, 50, and 99 are active
- Ports correctly assigned to respective VLANs
- No VLAN mismatch or pruning issues observed

---

## Trunk Verification

### Command
```cisco
show interfaces trunk
```

### Results
- Trunk established between SW1 and SW2
- VLANs 10,20,30,40,50,99 allowed
- Native VLAN set to 99
- All VLANs forwarding correctly

---

## EtherChannel Verification

### Command
```cisco
show etherchannel summary
```

### Results
- Port-Channel 1 is operational (SU state)
- LACP successfully negotiated
- Fa0/10 and Fa0/12 bundled correctly
- Load balancing active

---

## STP Verification

### Command
```cisco
show spanning-tree
```

### Results
- SW1 configured as root bridge for VLANs 10, 20, 30
- PortFast enabled on access ports
- BPDU Guard enabled on edge ports
- No switching loops detected

---

## DHCP Verification

### Command
```cisco
show ip dhcp binding
```

### Results
- Clients successfully receiving IP addresses
- DHCP pools active for VLANs 10–50
- Default gateways correctly assigned
- DNS servers correctly pushed (8.8.8.8 / 1.1.1.1)

---

## Inter-VLAN Routing Verification

### Test
Ping between VLANs

### Results
- Communication successful between all VLANs
- Router-on-a-Stick fully operational
- Default gateways responding correctly

---

## NAT / Internet Verification

### Commands
```cisco
show ip nat translations  
show ip nat statistics
```

### Results
- Inside networks successfully translated to WAN interface
- PAT (overload) working correctly
- Internet access confirmed via BT WiFi router

### External Connectivity Test
- Ping to 8.8.8.8 successful

---

## Port Security Verification (SW2)

### Command
show port-security interface fa0/15 (and others)

### Results
- Sticky MAC learning enabled
- Maximum MAC limit enforced per port
- Violation mode set to shutdown
- Errdisable recovery enabled for psecure-violation
- Security violations successfully triggered during testing

---

## Interface Status

### Command
```cisco
show ip interface brief
```

### Results
- All VLAN interfaces operational
- Trunk links up/up
- Management VLAN (VLAN 30) active on SW1 and SW2
- No critical interface failures

---

## Power over Ethernet (PoE) Verification

### Command
```cisco
show power inline
```

### Results
- PoE capability checked on SW2 access layer switches
- Voice VLAN ports (Fa0/14, Fa0/16, Fa0/18) configured for potential IP phone connectivity
- Power inline settings applied where supported
- No power faults or overload conditions observed

### Intended PoE Usage

- VLAN 50 (VOICE) designed for PoE-powered endpoints:
  - IP Phones
  - Wireless Access Points
  - Networked voice devices



