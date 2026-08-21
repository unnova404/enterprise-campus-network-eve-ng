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

## Network Topology

The laboratory implements a redundant three-tier enterprise campus network in EVE-NG. The topology consists of an edge router, two core switches, two distribution switches, and two access switches connecting four end devices.

![Network Topology](topology/network-topology.png)

### Topology Overview

The network is organized into the following layers:

| Layer        | Devices    | Primary Function                                                           |
| ------------ | ---------- | -------------------------------------------------------------------------- |
| Edge         | R1         | Internet connectivity, DHCP, NAT/PAT, and OSPF default-route advertisement |
| Core         | CSW1, CSW2 | Layer 3 routing and OSPF connectivity                                      |
| Distribution | DSW1, DSW2 | Inter-VLAN routing, HSRP, ACLs, OSPF, and STP control                      |
| Access       | ASW1, ASW2 | End-device connectivity, VLAN assignment, and Layer 2 security             |

The core layer provides redundant Layer 3 paths between the edge and distribution layers. The distribution layer provides the default gateways for the client VLANs and maintains redundancy through HSRP. The access layer connects end devices to the appropriate VLANs and applies Layer 2 security controls.

### Device Connections

The major connectivity relationships are:

* R1 connects to both CSW1 and CSW2 through routed Layer 3 links.
* CSW1 and CSW2 are interconnected through a Layer 3 LACP EtherChannel.
* CSW1 and CSW2 each have routed connections to DSW1 and DSW2.
* DSW1 and DSW2 are interconnected through a Layer 2 LACP EtherChannel configured as a trunk.
* DSW1 and DSW2 provide trunk connections toward the access switches.
* ASW1 and ASW2 provide access ports for the end devices.

This design provides multiple paths through the network and avoids dependence on a single core, distribution switch, or physical link.

### End-Device Connectivity

The access layer assigns end devices to different VLANs:

| Access Switch | Interface | VLAN | Network Role |
| ------------- | --------- | ---: | ------------ |
| ASW1          | Gi0/2     |   10 | USERS        |
| ASW1          | Gi0/3     |   20 | GUEST        |
| ASW2          | Gi0/2     |   10 | USERS        |
| ASW2          | Gi0/3     |   30 | IT           |

The access switches carry VLANs 10, 20, 30, and 99 through their trunk uplinks toward the distribution layer.
