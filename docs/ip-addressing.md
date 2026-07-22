# IP Addressing Scheme

## Overview 

This network utilizes a structured private IPv4 addressing scheme using the **10.10.x.0/24** address space
Each department is assigned to a dedicated subnet and VLAN to improve network segmentation, simpify
administration, and prepare the network for future security policies and access contorl.

Inter-VLAN routing is performed by the CISCO ISR 2911 router using **Router-on-a-Stick (802.1Q)**.
The first usable IP address within each subnet is reserved as the deault gateway.

---

# Network Addresssing Plan

| VLAN | Department | Network | Default Gateway | DHCP Scope |
|------|------------|---------|-----------------|------------|
| 10 | Management | 10.10.10.0/24 | 10.10.10.1 | 10.10.10.100 - 10.10.10.254 |
| 20 | IT | 10.10.20.0/24 | 10.10.20.1 |10.10.20.100 - 10.10.20.254 |
| 30 | Human Resources | 10.10.30.0/24 | 10.10.30.1 |10.10.30.100 - 10.10.30.254 |
| 40 | Finance | 10.10.40.0/24 | 10.10.40.1 |10.10.40.100 - 10.10.40.254 |
| 50 | Sales | 10.10.50.0/24 | 10.10.50.1 |10.10.50.100 - 10.10.50.254 |
| 60 | Servers | 10.10.60.0/24 | 10.10.60.1 |10.10.60.100 - 10.10.60.254 |
| 70 | Guest | 10.10.70.0/24 | 10.10.70.1 |10.10.70.100 - 10.10.70.254 |

---

# Static Infrastructure Addresses

| Device | IP Address | Purpose |
|--------|------------|---------|
| R1 (VLAN 10 Gateway) | 10.10.10.1 | Management Gateway |
| R1 (VLAN 20 Gateway) | 10.10.20.1 | IT Gateway |
| R1 (VLAN 30 Gateway) | 10.10.30.1 | HR Gateway |
| R1 (VLAN 40 Gateway) | 10.10.40.1 | Finance Gateway |
| R1 (VLAN 50 Gateway) | 10.10.50.1 | Sales Gateway |
| R1 (VLAN 60 Gateway) | 10.10.60.1 | Servers Gateway |
| R1 (VLAN 70 Gateway) | 10.10.70.1 | Guest Gateway |
| DC01 | 10.10.60.10 | Active Directory, DNS, DHCP |
| Printer 01 | 10.10.60.20 | Shared Network Printer |

*Setting DC01 Static IP address*
![DC01 Static IP Config](/screenshots/servers/DC01-static-ip.png)

---

# Addressing Strategy

- Each department is assigned an individual /24 subnet.
- The first usable address (.1) is reserved for the router gateway.
- Infrastructure devices utilize static IP addresses.
- End-user devices obtain addresses dynamically through DHCP.
- Network segmentation reduces broadcast traffic while improving security and manageability

