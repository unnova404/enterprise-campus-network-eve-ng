## Purpose

The purpose of this project is to design and implement a redundant three-tier enterprise campus network using EVE-NG. The network provides segmented user connectivity, dynamic routing, gateway redundancy, Internet access, centralized network services, and Layer 2 and Layer 3 security controls.

## Objectives

* Implement a three-tier enterprise campus network consisting of core, distribution, and access layers.
* Configure VLAN segmentation for USERS, GUEST, IT, and MANAGEMENT networks.
* Implement OSPF Area 0 for dynamic routing across the routed infrastructure.
* Implement HSRP to provide redundant default gateways for the VLANs.
* Implement LACP EtherChannel to provide link redundancy between network devices.
* Configure Rapid-PVST and distribute the STP root roles between the distribution switches.
* Configure centralized DHCP services on R1 and DHCP relay on the distribution switches.
* Implement NAT/PAT on R1 to provide Internet connectivity for the internal networks.
* Apply ACLs to control communication between internal VLANs.
* Implement Layer 2 security mechanisms including DHCP Snooping, Dynamic ARP Inspection, Port Security, PortFast, and BPDU Guard.
* Restrict administrative SSH access to the IT network.
* Verify network connectivity, routing, redundancy, network services, and security behavior within the EVE-NG environment.
