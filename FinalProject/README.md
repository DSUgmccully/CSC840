# Open Shortest Path First (OSPF) Route Injection
## General Information 
Author: Gary McCully<br>
Date: 12/7/2021<br>
Description: This is a presentation that covers the basics of exploiting a vulnerable OSPF configuration using a malicious pfSense box.<br>

## Why Should you care?
Open Shortest Route First (OSPF) is a popular Interior Gateway Protocol (IGP) that is used by many organizations. It enables routers to communicate with each other by ensuring packets are efficiently routed throughout an organization's network. Routers send OSPF path information to each other through the use of Link State Advertisements (LSA), and discover and maintain neighbor relationships through the use of HELLO packets. When a router goes offline, OSPF to identify a new path it can use to route packets within the network.<br>

Problems occur when LSA and HELLO packets are leaked to end-user and server networks rather than the routers that form the OSPF topology. When this occurs, it may be possible for a malicious attacker to insert malicious routes into the OSPF network. An attacker may insert a route that "blackholes" network traffic and brings the network to a halt. Additionally, an attacker may insert routes to cause traffic to flow through a malicious system that sniffs network traffic for sensitive information before forwarding it to its intended destination. Furthermore, an attacker may simply insert a route that completely hijack traffic destined for a different system and impersonate the intended recipient.<br>

The options available for authenticating routers within the OSPF network topology are rather weak and may be exploited by attackers. For example, the default authentication mechanism for OSPF is "null" when setting up OSPF using pfSense boxes. This means that any system able to send and receive LSA packets may have the ability to insert malicious routes into the OSPF topology without even needing a password. The second OSPF authentication type is the use of a clear-text password that is easily sniffed off the network. Finally, MD5 hashes may be used to authenticate LSA and HELLO packets, but tools exist that can crack these passwords offline. 

## Three Main Ideas
1. Routers are used to move network packets across the network to their intended recipient. To ensure packets are routed through the most efficient path possible, protocols such as OSPF are used within large organizations. OSPF also enables networks to "self-heal" in the event that one of the routers goes down.  
2. In many cases, OSPF is misconfigured and traffic that should only be sent and received by other routers within the OSPF topology can be sent and received by other network segments. These segments may include segments used for end-user computing or segments used by the organization's servers.
3. Even when the servers used within the OSPF topology use authentication, it may be possible for an attacker to insert malicious routes within the network topology that can result in a DoS condition, enable an attacker to view sensitive information, or impersonate a different system.

## Future Direction
At the time of this research there was only one tool that was commonly used for performing OSPF route injection attacks (Loki). However, this project has been all but abandoned and the dependencies cannot easily be located and installed on modern operating systems. Furthermore, the only tool other than Loki used to crack OSPF MD5 authentication is a tool named Cain and Abel. At the time of this research, the tool relied upon a driver used for sniffing network traffic that was would not install on Windows 10. Additionally, the website that was used to distribute the software no longer appears to be used for this purpose. The downloader can still be accessed using "The Way Back Machine," but it is obvious this tool is at end of life. Thus, attackers wishing to exploit weaknesses in OSPF will either need to create new tools for exploiting these weaknesses, or repurpose existing tools (e.g., pfSense) to perform these attacks.   

## Stream of Topics
Additional topics that may be related to OSPF exploitation include exploitation of other networking protocols that Loki was designed to attack. These include the following protocols:
- Address Resolution Protocol (ARP)
- Bidirectional Forwarding Detection (BFD)
- Border Gateway Protocol (BGP)
- Enhanced Interior Gateway Routing Protocol (EIGRP)
- Hot Standby Router Protocol (HSRP)
- Label Distribution Protocol (LDP)
- Multiprotocol Label Switching (MPLS)
- Routing Information Protocol (RIP)
- Virtual Router Redundancy Protocol (VRRP)
- WLAN Context Control Protocol (WLCCP)
## Additional Resources
- <a href="https://networklessons.com/ospf/ospf-lsa-types-explained">LSA Types</a>
- <a href="https://www.youtube.com/watch?v=oaZNOUZBXu0">OSPF Authentication Crack (Video)</a>
- <a href="https://www.rogerperkin.co.uk/ospf/ospf-authentication/">OSPF Authentication Types</a>
- <a href="https://learningnetwork.cisco.com/s/article/ospf-hello-and-lsa-packets">OSPF LSA and Hello Packets</a>
- <a href="https://docs.netgate.com/pfsense/en/latest/packages/frr/ospf/config-ospf.html">OSPF Tab Configuration</a>
- <a href="https://datatracker.ietf.org/doc/html/rfc2328#page-232">OSPF Version 2 RFC</a>
- <a href="http://cmdr-keen.blogspot.com/2015/05/widening-attack-landscape-with-ospf_3.html">Widening Attack Landscape with OSPF Route Injection</a>
