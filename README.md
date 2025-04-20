# Next-Gen Corporate Office Networking

This project demonstrates the configuration of VLANs, trunking, inter-VLAN routing, and DHCP pools for a corporate office network setup. The project involves multiple networking tasks to ensure proper network segmentation, communication between different VLANs, and dynamic IP assignment using DHCP.

## Table of Contents
- [VLAN Configuration](#vlan-configuration)
- [Trunk Configuration](#trunk-configuration)
- [Inter-VLAN Routing](#inter-vlan-routing)
- [DHCP Configuration](#dhcp-configuration)
- [Excluded IP Ranges](#excluded-ip-ranges)
- [Verification Commands](#verification-commands)

---

## VLAN Configuration

### Steps:
1. **Create VLANs**:
    - VLAN 10 (IT)
    - VLAN 20 (HR)
    - VLAN 30 (FIN)

```shell
Switch(config)# vlan 10
Switch(config-vlan)# name IT
Switch(config-vlan)# exit

Switch(config)# vlan 20
Switch(config-vlan)# name HR
Switch(config-vlan)# exit

Switch(config)# vlan 30
Switch(config-vlan)# name FIN
Switch(config-vlan)# exit
```
Assign Ports to VLAN 10:

Ports fa0/2 to fa0/24 are assigned to VLAN 10.


Switch(config)# interface range fa0/2 - 24
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
Switch(config-if-range)# exit
Trunk Configuration
Configure Trunk Ports (gig1/0/1-4):

Ports gig1/0/1 to gig1/0/4 are set as trunk ports to allow multiple VLANs.


Switch(config)# interface range gig1/0/1-4
Switch(config-if-range)# switchport mode trunk
Switch(config-if-range)# exit
Trunk Configuration on Port fa0/1:

fa0/1 is set as a trunk port to carry traffic for multiple VLANs.


Switch(config)# interface fa0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# exit
Inter-VLAN Routing
Configure Router Interfaces:

Created sub-interfaces gig0/0.10, gig0/0.20, and gig0/0.30 for VLAN 10, 20, and 30 respectively.


Router(config)# int gig0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.1.1 255.255.255.0

Router(config)# int gig0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.2.1 255.255.255.0

Router(config)# int gig0/0.30
Router(config-subif)# encapsulation dot1Q 30
Router(config-subif)# ip address 192.168.3.1 255.255.255.0
DHCP Configuration
Configure DHCP Pools:

Configured DHCP pools for each VLAN to provide dynamic IP addresses.


Router(config)# ip dhcp pool IT-pool
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 192.168.1.1

Router(config)# ip dhcp pool HR-pool
Router(dhcp-config)# network 192.168.2.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.2.1
Router(dhcp-config)# dns-server 192.168.2.1

Router(config)# ip dhcp pool FIN-pool
Router(dhcp-config)# network 192.168.3.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.3.1
Router(dhcp-config)# dns-server 192.168.3.1
Excluded IP Ranges
Exclude IP Ranges:

Excluded IP ranges from being assigned by the DHCP server.

Router(config)# ip dhcp excluded-address 192.168.1.1 192.168.1.10
Router(config)# ip dhcp excluded-address 192.168.2.1 192.168.2.10
Router(config)# ip dhcp excluded-address 192.168.3.1 192.168.3.10
Verification Commands
Verify Trunk Configuration:


Switch# show interfaces trunk
Check VLAN Configuration:

Switch# show vlan brief
Verify DHCP Settings:


Router# show ip dhcp pool
Check DHCP Lease Information:


Router# show ip dhcp binding
Check Interface Status:


Router# show ip interface brief
Conclusion
This project successfully implements the core components of a next-generation corporate office network by configuring VLANs, trunk ports, inter-VLAN routing, and DHCP services. The configuration ensures proper communication between different VLANs, dynamic IP assignment, and network segmentation for enhanced security and performance.

## Author
Md. Junayed Bin Karim
Student, BSc in Computer Science and Engineering (CSE)
Daffodil International University, Bangladesh
