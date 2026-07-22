# Device Inventory

## Overview 

This document provides an inventory of all hardware devices used throughout this Lab

---

# Network Devices 

| Hostname | Device | Model | Purpose |
|----------|--------|-------|---------|
| R1 | Router | Cisco 2911 ISR | Inter-VLAN routing using Router-on-a-Stick |
| SW-Core | Core Switch | Cisco Catalyst 2960 | Aggregates network infrastructure and trunk links |
| SW-Office1 | Access Switch | Cisco Catalyst 2960 | Provides connectivity for IT, HR, and Finance departments |
| SW-Office2 | Access Switch | Cisco Catalyst 2960 | Provides connectivity for Sales, and Management departments |
| DC01 | Server | Server-PT | Centralized DHCP Server |
| Printer01 | Printer | Printer-PT | Shared network printer |

---

# End User Devices

| Devices | Department | Addressing |
|---------|------------|------------|
| PC-IT01 | Information Technology | DHCP |
| PC-IT02 | Information Technology | DHCP |
| PC-HR01 | Human Resources | DHCP |
| PC-HR02 | Human Resources | DHCP |
| PC-FIN01 | Finance | DHCP |
| PC-FIN02 | Finance | DHCP |
| PC-SALES01 | Sales | DHCP |
| PC-SALES02 | Sales | DHCP |
| PC-MGMT01 | Management | DHCP |
| PC-MGMT02 | Management | DHCP |

---

# Infrastructure Services

| Service | Device |
|---------|--------|
| Inter-VLAN Routing | R1 |
| VLAN Switching | SW-Core |
| Access Layer Switching | SW-Office1 / SW-Office2 |
| DHCP | DC01 |
| Network Printing | Printer01 |

---

# Design Summary

The network follows a hierarchical design consisting of a central Layer 2 core switch, two access-layer switches, and an edge router providing inter-VLAN routing through Router-on-a-Stick.
