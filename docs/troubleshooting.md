# Troubleshooting

## Overview

This document records issues encountered during implementation and the steps taken to resolve them.

---

# Issue 1

## Native VLAN Mismatch

### Symptoms

Switch reported a native VLAN mismatch warning during configuration.

### Cause

An uplink between switches was accidentally connected to an access interface and assigned to a user VLAN.

### Resolution

- Re-cabled the uplink using the appropriate Gigabit interface.
- Configured both ends of the link as 802.1Q trunk ports.
- Verified operation using:
  
```
show interfaces trunk
```

# Issue 2

## Server Unreachable

### Symptoms

Clients successfully reached router gateways but could not communicate with DC01.

### Cause

Server switch ports remained assigned to VLAN 1 instead of Server VLAN

### Resolution

Assigned the correct switch ports to VLAN 60.

Verified communication using ping and taking note of successful ICMP requests.

---

# Issue 3

## Incorrect DHCP Scop Assignment

### Symptoms

One IT workstation received an IP address from the HR subnet.

### Cause 

The workstation was physically connected to a switch port assigned to VLAN 30

### Resolution

Corrected the physical cabling to match the documented network design.

Renewed the DHCP lease and confirmed the workstation received an address from the IT DHCP scope.

---

# Issue 4

## Router Link Down

### Symptoms

Router interface remained down and the rouer failed to appear in CDP neighbor discovery.

### Cause

The router interface was administratively shutdown

### Resolution

Enabled the interface using:

```
interface GigabitEthernet0/0
no shutdown
```

Verfied operation using:

```
show ip interface brief
```

---

# Issue 5

## Router Trunk Configuration

### Symptoms

Inter-VLAN routing failed

### Cause

The switch interface connected to the router was not configured as an 802.1Q trunk.

### Resolution

Configured the switch interface as a trunk an verified the allowed VLANs using:

```
show interface trunk
```

---

# Lessons Learned

Throughout implementation several important network conecpts were reinforced:

- Proper physical cabling is just as important as logical configuration.
- DHCP assigns addresses based on VLAN membership, not device names.
- Router-on-a-Stick requires both trunk ports and correctly configured subinterfaces.
- Validation should be performed after each major configuration step to simplify troubleshooting
