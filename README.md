# 🌐 Packet Tracer Network Lab - Corporate Network with Enhanced Security and Services
=================================================

## 📌 Description
-----------
  This project simulates an enhanced corporate network environment, building upon a 
  previous design to incorporate new security features and services. It demonstrates the 
  implementation of a scalable and resilient network for a main office, a branch office, 
  and a dedicated DMZ (demilitarized zone), showcasing real-world concepts like dynamic 
  routing (OSPF), various NAT configurations, a Site-to-Site VPN, and detailed access control 
  lists (ACLs). 
   
## 🎯 Objectives
----------
- Configure VLANs to logically segment the network for traffic isolation and enhanced security.

- Implement dynamic routing using OSPF for both IPv4 and IPv6 to ensure network 
  scalability and efficiency.
    
- Set up multiple Network Address Translation (NAT) types, including 
  PAT (Port Address Translation) for internal networks and Static NAT for server access 
  in the DMZ.

- Establish a secure Site-to-Site VPN connection between the main office and the branch 
  office using an IPsec-protected GRE Tunnel.
  
- Integrate IPv6 using SLAAC and DHCPv6 to support modern internet protocols.

- Apply comprehensive Access Control Lists (ACLs) to control and restrict traffic between 
  different network segments and from the internet.

- Configure a Demilitarized Zone (DMZ) to securely host public-facing servers.

- Implement Port Security on switches to prevent unauthorized devices from connecting to 
  the network.

## 🛠 Equipment Used
--------------
- 2x Cisco 2911 Router
- 2x Cisco 2960 Switch
- 1x Cisco 2911 Router (as ISP)
- 1x Server-PT (as DNS Server)
- 3x PC, 1x Laptop
- Cisco Packet Tracer 8.2.2.0400

## Key Concepts
------------
- VLANs (Virtual Local Area Networks): The network is logically segmented into three distinct VLANs to isolate traffic and reduce broadcast domains. 
  VLAN 10 and VLAN 20 are in the main office, while VLAN 30 is in the branch office.

- Router-on-a-Stick: On both routers, a single physical interface is configured with logical sub-interfaces to route traffic between the VLANs, 
  optimizing resource usage.

- NAT (Network Address Translation): A form of NAT called Port Address Translation (PAT) is configured on Router1 to translate private IPv4 addresses into a single public address, 
  enabling all internal devices to communicate with the Cloud.

- IPv6: The network is configured with SLAAC (Stateless Address Autoconfiguration), allowing devices to automatically generate their own unique IPv6 addresses, 
  simplifying network management.
  
- Dynamic Routing (OSPF): Instead of static routes, OSPF is configured for both IPv4 and IPv6 (OSPFv2 and OSPFv3) to allow the routers to automatically discover and share routing information, 
  ensuring the network is scalable and resilient to topology changes.
  
- GRE Tunnel: A secure, site-to-site tunnel is established between the main office and the branch office.

- ACLs (Access Control Lists): A security rule is implemented on Router1 to explicitly deny communication from VLAN 10 to VLAN 20, while permitting all other traffic.

- QoS: Traffic from a specific VLAN is prioritized to guarantee a certain level of performance.

## 🔧 Configuration Summary
---------------------
- Router1 (Main Office)

  + Routing: Handles inter-VLAN routing for VLAN 10, VLAN 20, and the new DMZ (VLAN 99).
  
  + NAT: Configured with PAT for internal subnets (VLAN10, VLAN20, DMZ_SERVERS) and Static NAT to map a server's private IP (192.168.99.10) to a public IP (209.165.200.10).
  
  + VPN: Acts as one endpoint of an IPsec-protected GRE tunnel with Router2.
  
  + Security: Implements an extended ACL (BLOCK_PC1_PC2) on its GigabitEthernet0/0.10 interface to block specific ICMP traffic, and an ACL (VPN_TRAFFIC) to control which traffic is 
    encrypted by the VPN.
  
  + WAN: Connects to the ISP via GigabitEthernet0/2, with a public IP address.
  
- Router2 (Branch Office)

  + Routing: Manages the branch office network and participates in OSPF with Router1.
  
  + VPN: Acts as the second endpoint of the IPsec-protected GRE tunnel.
  
  + Security: Uses an ACL (VPN_TRAFFIC) to identify traffic that needs to be routed through the secure tunnel.
  
- Switch1 & Switch2

  + VLANs: Switch1 is configured with VLAN 10 and 20, while Switch2 has VLAN 30.
  
  + Trunk Ports: FastEthernet0/24 on both switches is configured as a trunk port to carry traffic for their respective VLANs.
  
  + Port Security: Implemented on access ports to restrict device connections to a single, sticky MAC address.
  
- ISP Router

  + WAN: Simulates an internet service provider, with connections to both the main office (Router1) and the DNS server.
  
  + Routing: Uses a static route to direct traffic for the corporate network (192.168.0.0/16) back to Router1.

# Project Evolution: Key Additions and Changes
---------------------
 This project significantly expands the previous network by adding new devices and configurations, making the topology more realistic and secure.

- Dedicated ISP Router: A new Cisco 2911 router, named "ISP", has been introduced to simulate a real-world internet service provider. It replaces the simple "Cloud" device, providing more 
realistic routing and connectivity.


- Static and PAT NAT: Router1 now features two distinct NAT configurations:

	+ PAT (Port Address Translation) is used for the internal VLANs (VLAN 10 and VLAN 20), allowing all devices to access the internet using a single public IP address.

	+ Static NAT is configured for a web server in the DMZ, mapping its private IP address to a specific public IP address, making it accessible from the internet while keeping its 
	  internal address private.


- DMZ (Demilitarized Zone): A new VLAN (VLAN 99) has been created to act as a DMZ. This isolated network segment is designed to host servers that must be accessible from the internet but 
separated from the internal corporate network, providing an additional layer of security.

- IPsec-protected GRE Tunnel: Instead of a simple GRE tunnel, this project uses an IPsec overlay to encrypt the tunnel traffic. This creates a secure, Site-to-Site VPN, ensuring 
confidential communication between the main and branch offices.

- Advanced ACLs: New ACLs have been implemented to control traffic with more granularity. For example, an ACL now explicitly denies ping traffic between specific hosts (PC1 and PC2) 
to simulate a real security policy.

## 📷 Screenshots
-----------
- Network Diagram: diagram.png
- PC3 Ping Test: screenshots/ping_test_pc3_to_dns_server.png

## 🚀 How to Run
----------
1. Open corporate_network_project.pkt in Cisco Packet Tracer.
2. Start the simulation and wait for all devices to boot up.
3. Verify network connectivity by pinging devices across different VLANs and to the internet.

## Summary
-------
This project represents a significant step forward in network design, moving from a basic setup to a complex and realistic corporate environment. By adding a dedicated ISP, a DMZ, 
and an IPsec-protected VPN, it demonstrates advanced skills in network configuration, security, and troubleshooting.
=================================================
# Author: Serhii Gorin 
# Date: 03.09.2025
