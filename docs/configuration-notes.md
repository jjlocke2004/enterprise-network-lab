# Configuration Notes

## Project Overview

This document summarizes the major configuration tasks completed while building the out network.

---

# Initial Device Configuration

The following baseline configuration was applied to all Cisco networking devices:

- Hostnames configured
- DNS lookup disabled
- Console password configured
- Configurations saved to startup configuration
  
![Basic Device Config](/screenshots/device-management/basic-device-config.png)

---

# VLAN Configuration

The network was segmented into seven VLANs:

| VLAN | Name |
|------|------|
|10|Management|
|20|IT|
|30|HR|
|40|Finance|
|50|Sales|
|60|Servers|
|70|Guest|

VLANs were created on the core switch and both access switches

---

# Access Ports

Department workstations were assigned to dedicated VLANs using access ports.

Each access switch was configured according to the network design documentation.

---

# Trunk Links

802.1Q trunk links were configured between:

- R1 ↔ SW-Core
- SW-Core ↔ SW-Office1
- SW-Core ↔ SW-Office2

These links transport traffic for all configured VLANs.

---

# Router-on-a-Stick

Inter-VLAN routing was implemented using Router-on-a-Stick

Each VLAN was assigned:
- Dedicated subinterface
- 802.1Q encapsulation
- Default gateway

---

# DHCP

A centralized DHCP server was configured on DC01.

Seperate DHCP scopes were created for each client VLAN.

The router forwards DHCP broadcasts using the 'ip helper-address' command.

Infrastructure devices reamin statically addressed.

---

# Validation

The follwing functionality was successfully verified:

- VLAN segmentation
- Trunk communication
- Inter-VLAN routing
- DHCP address assignment
- Cross-VLAN connctivity
- Server communication
- Network printer communication

