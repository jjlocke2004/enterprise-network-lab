# DHCP Configuration

## Overview

Centralized DHCP services were configured on **DC01** to dynamically assign IPv4 addressing 
information to client workstations across multiple VLANs

Because DHCP requests are broadcast-based and do not cross router boundaries by default, 
the Cisco ISR 2911 router was configured as a DHCP relay using the 'ip helper-address' command 
on each client-facing VLAN subinterface

Infrastructure devices such as DC01 and Printer01 use static IP addresses and are NOT assigned
addresses through DHCP.

---

## DHCP Server

DC01 is configured with the following static network settings:

| Setting | Value |
|---------|-------|
| IP Address | '10.10.60.10' |
| Subnet Mask | '255.255.255.0' |
| Default Gateway | '10.10.60.1' |
| VLAN | '60 - SERVERS' |

The DHCP service was enabled through the Packet Tracer Server-PT services interface.

*Its challenging to see because of the light text and light background but near the top - DHCP service shows 'On' is checked*

![DHCP Server and Pool Configuration](/screenshots/dhcp/dhcp-enabled-and-pool.png)

---

## DHCP Scope Design

Seperate DHCP pools were created for each client VLAN.

| Pool Name | VLAN | Network | Default Gateway | Starting Address |
|-----------|------|---------|-----------------|------------------|
| MANAGEMENT | 10 | '10.10.10.0/24' | '10.10.10.1' | '10.10.10.100' |
| IT | 20 | '10.10.20.0/24' | '10.10.20.1' | '10.10.20.100' |
| HR | 30 | '10.10.30.0/24' | '10.10.30.1' | '10.10.30.100'|
| FINANCE | 40 | '10.10.40.0/24' | '10.10.40.1' | '10.10.40.100' |
| SALES | 50 | '10.10.50.0/24' | '10.10.50.1' | '10.10.50.100' |
| GUEST | 70 | '10.10.70.0/24' | '10.10.70.1 | '10.10.70.100' |

VLAN 60 does not use a client DHCP scope because the server and printer are assigned static addresses.

---

## DHCP Relay Configuration

The router forwards DHCP requests from each client VLAN to DC01 using:

```cisco
ip helper-address 10.10.60.10
```

The command was applied to these subinterfaces:

| Router Subinterface | VLAN |
|---------------------|------|
| GigabitEthernet0/0.10 | 10 |
| GigabitEthernet0/0.20 | 20 |
| GigabitEthernet0/0.30 | 30 |
| GigabitEthernet0/0.40 | 40 |
| GigabitEthernet0/0.50 | 50 |
| GigabitEthernet0/0.70 | 70 |

A helper address was NOT needed for VLAN 60 since DC01 is directly connected to that subnet.

![DHCP Relay Config](/screenshots/dhcp/dhcp-relay.png)

---

## Client Address Assignement

After the DHCP server and relay configuration were completed, 
client workstations were chnaged from static addressing to DHCP.

Each workstation received an address from the scope associated with the VLAN assigned to its switch port.

Example IT client configuration:

| Setting | Assigned Value |
|---------|----------------|
| IPv4 Address | '10.10.20.100' or later |
| Subnet Mask | '255.255.255.0' |
| Default Gateway | '10.10.20.1 |
| DHCP Server | '10.10.60.10' |

*DHCP working on PC-IT01 (checked for all endpoints)*

![DHCP Client Address](/screenshots/dhcp/dhcp-client-address.png)

---

## Validation

DHCP operation was verified by confirming that:

- Each worksation received an address from the correct departmnetal subnet.
- The assigned default gateway matched the router subinterface for that VLAN.
- Clients could reach their default gateway.
- Clients could communicate with DC01.
- Inter-VLAN connectivity continuous to function after clients switched to DHCP.

During testing, one of the IT workstations initially received an HR IP address because 
it was physically connected to a switch port assigned to VLAN 30.
The cabling was corrected, the DHCP lease was renewed, and the workstation 
then received an address from the IT scope.

---

## Result

Centralized DHCP successfully provides automatic IPv4 configuration to all client VLANs, 
while DHCP relay enabled requests to cross VLAN boundaries and reach DC01 in the Server VLAN.
