# ACL Configuration
Access Control List Configuration

## Overview

To further segment and secure this simulated enterprise network, 
three access control lists were implemented on the router.
These ACLs enforce least-privilege access between departments, restrict management plane access, 
and protect sensitive department resources from unauthorized inter-VLAN traffic.

---

## ACL 1 - Guest VLAN isolation

**Purpose:** Prevent the Guest VLAN from reaching any internal department subnet while still allowing
general outbound connectivity. (Internet Access)

**Applied on:** Guest subinterface, inbound direction

*I ran this on the router R1 to configure the ACL*

![Configuring Guest ACL on R1](../screenshots/access-control-list/configuring-r1-with-guest-acl.png)

**Validation:**
I created a Guest PC and connected it to the office switch #2

From the SWOffice2 I configured the connection to the Guest PC

![Configuring Connection from SWOffice2 to Guest-PC](../screenshots/access-control-list/configuring-connection-from-swoffice2-to-guest-pc.png)

I then switched the IP Config on the Guest PC to DHCP and verified it got an appropriate IP address.

![Switching To DHCP on Guest PC](../screenshots/access-control-list/switching-to-dhcp-on-guest-pc-success.png)

I then tried pinging tested the ACL from the Guest PC by first pinging the Guest VLAN Gateway which succeeded as expected.
Then I tried pinging an IT PC and a Finance PC which both returned with host unreachable. That is the exact behavior I was looking to achieve

![Verifying Guest VLAN ACL from Guest PC](../screenshots/access-control-list/verifying-guest-vlan-acl-from-guest-pc.png)
