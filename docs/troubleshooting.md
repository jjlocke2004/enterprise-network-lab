# Troubleshooting

## Overview

Throughout the implementation of the Enterprise Network Lab, several configuration and connectivity issues were encountered while deploying VLAN segmentation, inter-VLAN routing, centralized DHCP, and basic network security controls.

Each issue was identified, isolated, and resolved using Cisco IOS verification commands and systematic troubleshooting techniques. Documenting these issues provides a record of the deployment process while demonstrating practical problem-solving throughout the project.

---

# Native VLAN Mismatch Warning

## Problem

A native VLAN mismatch warning appeared after configuring switch interfaces.

## Cause

One side of a trunk link was temporarily configured differently than the other during the trunk configuration process.

## Resolution

Both interfaces were verified and configured as IEEE 802.1Q trunk ports with matching settings. Trunk operation was confirmed using:

```cisco
show interfaces trunk
```

---

# Router Interface Administratively Down

## Problem

The router-to-core switch connection remained down, preventing inter-VLAN communication.

## Cause

The physical router interface had not yet been enabled after configuration.

## Resolution

The interface was enabled using:

```cisco
interface GigabitEthernet0/0
 no shutdown
```

The interface status was verified using:

```cisco
show ip interface brief
```

Once enabled, connectivity between the router and core switch was restored.

---

# Incorrect Server VLAN Assignment

## Problem

The domain controller (DC01) and shared network printer were initially assigned to incorrect switch interfaces.

## Cause

The switch port assignments did not match the intended network topology.

## Resolution

The server and printer were moved to the appropriate access ports assigned to VLAN 60 (SERVERS). The VLAN assignment was verified using:

```cisco
show vlan brief
```

---

# Incorrect Physical Cabling

## Problem

One Information Technology workstation received an IP address from the Human Resources subnet.

## Cause

The workstation was physically connected to a switch port assigned to VLAN 30 instead of VLAN 20.

## Resolution

The physical cable was moved to the correct access port, the DHCP lease was renewed, and the workstation successfully received an address from the Information Technology DHCP scope.

---

# DHCP Relay Configuration

## Problem

Client workstations located on remote VLANs were unable to obtain IP addresses from the centralized DHCP server.

## Cause

DHCP broadcast traffic does not cross Layer 3 boundaries by default.

## Resolution

The `ip helper-address` command was configured on each client-facing router subinterface to forward DHCP requests to DC01.

Following implementation, clients successfully received addresses from their respective DHCP scopes.

---

# Switch Management Interfaces

## Problem

The switches initially lacked management IP addresses, preventing centralized remote administration.

## Cause

No Switch Virtual Interface (SVI) or default gateway had been configured.

## Resolution

A management interface was configured on VLAN 10 for each switch, and the appropriate default gateway was assigned.

Management connectivity was verified after configuration.

---

# SSH Remote Management

## Problem

Network devices could only be managed through the local console connection.

## Cause

SSH had not yet been configured.

## Resolution

Each network device was configured with:

- Local administrator account
- Enterprise domain name
- 2048-bit RSA encryption keys
- SSH Version 2
- VTY lines restricted to SSH only

Successful SSH configuration was verified using:

```cisco
show ip ssh
```

---

# Access Port Security

## Problem

Switch access ports initially accepted any connected device without restriction.

## Cause

Port Security had not yet been implemented.

## Resolution

Port Security was configured on all access ports using:

- Maximum of one MAC address
- Sticky MAC address learning
- Restrict violation mode

Configuration was verified using:

```cisco
show port-security
```

---

# Unused Switch Interfaces

## Problem

Unused switch interfaces remained enabled after the initial network deployment.

## Cause

Cisco switches leave unused interfaces enabled by default.

## Resolution

Unused interfaces were administratively shut down and reserved for future expansion, reducing the attack surface of the network.

---

# Lessons Learned

This project reinforced several important networking concepts:

- Physical topology and logical topology must remain synchronized.
- DHCP address assignment depends on VLAN membership rather than device names.
- Router-on-a-Stick requires correctly configured router subinterfaces and operational trunk links.
- Incremental testing after each major configuration change significantly reduces troubleshooting time.
- Maintaining accurate documentation throughout implementation improves deployment consistency and simplifies future maintenance.

---

# Validation

Following implementation and troubleshooting, the completed network successfully demonstrated:

- VLAN segmentation
- IEEE 802.1Q trunking
- Router-on-a-Stick inter-VLAN routing
- Centralized DHCP deployment
- DHCP relay functionality
- Correct client address assignment
- Client-to-server communication
- Client-to-printer communication
- SSH remote management
- Switch management interfaces
- Port Security
- Administrative shutdown of unused switch interfaces
