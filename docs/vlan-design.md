# VLAN Design

## Overview

The network is logically segmented using Virtual Local Area Networks (VLANs).
Each department is assigned a dedicated VLAN to isolate broadcast domains, improve perfomance.
and prepare the network for future security policies such as Access Control Lists (ACLs)

Inter-VLAN communication is provided by a Cisco ISR 2911 router configured using Router-on-a-Stick (802.1Q encapsulation).

---

# VLAN Assignment

| VLAN ID | VLAN Name | Department | Subent |
|---------|-----------|------------|--------|
| 10 | MANAGEMENT | Management | 10.10.10.0/24 |
| 20 | IT | Inforamtion Technology | 10.10.20.0/24 |
| 30 | HR | Human Resources | 10.10.30.0/24 |
| 40 | FINANCE | Finance | 10.10.40.0/24 |
| 50 | SALES | Sales | 10.10.50.0/24 |
| 60 | SERVERS | Server Infrastructure | 10.10.60.0/24 |
| 70 | GUEST | Guest Devices | 10.10.70.0/24 |

---

# Switch Port Assignments

## SW-Office1

| Interface | Connected Device | VLAN |
|-----------|------------------|------|
| Fa0/1 | PC-IT01 | 20 |
| Fa0/2 | PC-IT02 | 20 |
| Fa0/3 | PC-HR01 | 30 |
| Fa0/4 | PC-HR02 | 30 |
| Fa0/5 | PC-FIN01 | 40 |
| Fa0/6 | PC-FIN02 | 40 |

---

## SW-Office2 

| Interface | Connected Device | VLAN |
|-----------|------------------|------|
| Fa0/1 | PC-SALES01 | 50 |
| Fa0/2 | PC-SALES02 | 50 |
| Fa0/3 | PC-MGMT01 | 10 |
| Fa0/4 | PC-MGMT02 | 10 |

---

## SW-Core

| Interface | Connected Device | VLAN |
|-----------|------------------|------|
| Fa0/23 | DC01 | 60 |
| Fa0/24 | Printer01 | 60 |

---

# Trunk Links
| Connection | Purpose |
|------------|---------|
| R1 ↔ SW-Core | Router-on-a-Stick trunk carrying all VLANs | 
| SW-Core ↔ SW-Office1 | 802.1Q trunk carrying all VLAN traffic |
| SW-Core ↔ SW-Office2 | 802.1Q trunk carrying all VLAN traffic |

---

# Design Consideration

- Departmental traffic is segmented using dedicated VLAN.
- Server infrastructure is isolated the domain controller
  and network printer, are centrally connected to the core swtich
- Trunk links carry traffic for all VLANs between network devices.
- This design provides a scalable foundation for implementing
  DHCP, ACLs, SSH management, and additional enterprise security controls.
