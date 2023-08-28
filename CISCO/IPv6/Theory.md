IPv6 : 16 Octects : 128 bits 
IPv4 : 4 Octects : 32 bits

| Network Prefix | Interface identifier |
|---|---|
| 64 bits | 64 bits |

In IPv6 all interfaces have a /64 mask. There's not subnetting in IPv6. There's no need for NAT either.

#### Format

X:X:X:X:X:X:X:X     where X = 16 bit Hexadecimal field

E.g.
2001:0000:13Of:0000:0000:09d0:876a:123B

**Format Rules**
- Leading zeros are optional
- Succesive fields of zeros can be represented as ::
	- But only once per address

Following these rules, we could write the example above as follows:

2001:0:130f::09d0876a:123B

#### URLs
When using IPv6 on a Web Browser, you need to enclose the IPv6 address in square brackets.
E.g.
https:// \[2001:123:4567::8\]:8080/index.html



Case insensitive

### IPv6 Unicast Addresses

- Unspecified
	::/128

- Loopback
	::1/128

- Aggregate Global
	2001::/16
	2002::/16
	3FFE3::/16
	(There's no need for NAT with IPv6)

- Link Local
	FE80::/10
	Collision Domain scope. (Used by routing protocols)

- Site Local
	FEC0::/10
	LAN scope. No routable on the internet (Deprecated)

- IPv4 Compatible
	0:0:0:0:0:0::/96
	(Deprecated)

#### IPv6 EUI addresses
All Agregate Global IP addresses have a Network Prefix of 64.

| Network Prefix | Interface Identifier |
|---|---|
| 64 bits | 64 bits |

The interface ID can use Modified EUI-64 format
E.g.
![[Screenshot 2023-02-20 at 18.15.27.png]]

![[Screenshot 2023-02-20 at 18.31.22.png]]





### IPv6 Multicast Addresses

- Assigned
	FF00::/8

- Solicited-Node
	FF02::1:FF00:0000/104

- To All Local Hosts
	FF02::1
	Destination IPv6 address in router advertisements

- To All Routers
	FF02::2
	Destination IPv6 address in host solicitations

- To All DHCPv6 agents
	FF02::1:2
	Destination IPv6 address in DHCP solicit messages 

### IPv6 Routing types
- Static
- RIPng (RFC 2080)
- OSPFv3 (RFC 2740)
- IS-IS for IPv6
- MP-BGP4 (RFC 2545/2858)
- EIGRP for IPv6

In CISCO routers, you need to run `ipv6 unicast-routing` before you can configure any routing protocol.