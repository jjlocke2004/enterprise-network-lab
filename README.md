# Enterprise Network Lab

## Overview

This project simulates a small enterprise network built entirely in Cisco Packet Tracer. The objective was to design, configure, validate, and document a segmented network using industry-standard networking concepts including VLANs, Router-on-a-Stick inter-VLAN routing, centralized DHCP, and enterprise network documentation.

Rather than focusing solely on connectivity, this project emphasizes proper network planning, documentation, implementation, and validation to mirror the workflow used during real infrastructure deployments.

---

## Project Objectives

- Design a scalable enterprise network topology
- Implement departmental network segmentation using VLANs
- Configure Layer 2 switching and IEEE 802.1Q trunking
- Implement Router-on-a-Stick inter-VLAN routing
- Deploy centralized DHCP services
- Validate connectivity across multiple network segments
- Produce professional implementation documentation

---

## Network Overview

### Devices

- Cisco ISR 2911 Router
- Cisco Catalyst 2960 Core Switch
- Two Cisco Catalyst 2960 Access Switches
- DHCP Server (DC01)
- Network Printer
- Ten Department Workstations

### Departments

- Management
- Information Technology
- Human Resources
- Finance
- Sales
- Servers
- Guest

---

## Implemented Features

- VLAN Segmentation
- Access Port Configuration
- 802.1Q Trunk Links
- Router-on-a-Stick
- Inter-VLAN Routing
- Centralized DHCP
- Static Infrastructure Addressing
- Network Validation and Testing

---

## Repository Structure

```text
Enterprise-Network-Lab/
│
├── README.md
│
├── docs/
│   ├── ip-addressing.md
│   ├── vlan-design.md
│   ├── device-inventory.md
│   ├── configuration-notes.md
│   └── troubleshooting.md
│
├── screenshots/
│   ├── topology/
│   ├── switching/
│   ├── routing/
│   ├── dhcp/
│   └── validation/
│
└── Enterprise-Network-Lab.pkt
```

---

# Documentation

Detailed implementation documentation is organized within the `docs` directory.

| Document | Description |
|-----------|-------------|
| **![ip-addressing.md](docs/ip-addressing.md)** | IP addressing plan, subnet allocation, gateways, and DHCP scopes |
| **![vlan-design.md](docs/vlan-design.md)** | VLAN assignments, switch port mappings, and trunk design |
| **![device-inventory.md](docs/device-inventory.md)** | Inventory of all network devices and infrastructure |
| **![configuration-notes.md](docs/configuration-notes.md)** | Summary of configuration tasks completed throughout implementation |
| **![troubleshooting.md](docs/troubleshooting.md)** | Common issues encountered during deployment and their resolutions |

---

## Screenshots

Project screenshots are organized by implementation phase.

- Network Topology
- Switch Configuration
- Router Configuration
- DHCP Configuration
- Validation Testing

---

## Skills Demonstrated

### Networking

- VLAN Design
- Layer 2 Switching
- IEEE 802.1Q Trunking
- Router-on-a-Stick
- Inter-VLAN Routing
- DHCP Deployment
- IP Address Planning
- Enterprise Network Documentation

### Cisco IOS

- Interface Configuration
- VLAN Management
- Trunk Configuration
- Router Subinterfaces
- DHCP Relay (ip helper-address)
- Network Validation
- Configuration Management

---

## Validation

The completed network was validated by successfully verifying:

- VLAN segmentation
- Trunk connectivity
- Inter-VLAN routing
- DHCP address assignment
- Client-to-server communication
- Client-to-printer communication
- Cross-department connectivity

---

## Future Improvements

The following features will be implemented during the next phase of the project:

- SSH Remote Management
- Port Security
- Switch Management Interfaces
- Login Banner (MOTD)
- Unused Port Hardening
- Access Control Lists (ACLs)

---

## Project Status

**Current Status:** In Progress

✔ Enterprise network architecture completed

✔ Layer 2 switching completed

✔ Router-on-a-Stick implemented

✔ Centralized DHCP implemented

✔ Network validation completed

⬜ Security hardening (in progress)

⬜ SSH management

⬜ ACL implementation

⬜ Port security
