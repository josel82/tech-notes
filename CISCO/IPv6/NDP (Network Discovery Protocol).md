
 
The ARP-like function of NDP uses IPv6 and Solicited-Node multicast to learn the MAC address of other hosts
Two message type are used for this:
1. Neighbor Solicitation (NS) = ICMPv6 Type 135
2. Neighbor Advertisement (NA) = ICMPv6 Type 136


Another function of NDP allows hosts to automatically discover routers on the local network.
Two message type are used for this:
1. Router Solicitation (RS) = ICMPv6 Type 133 (sent to ff02::2 - all routers)
2. Router Advertisement (RA) = ICMv6 Type 134 (sent to ff02::1 - all nodes)
