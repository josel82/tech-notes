# Definitions
#Networking #IT 

IPv6 : 16 Octects : 128 bits 
IPv4 : 4 Octects : 32 bits

| Network Prefix | Interface identifier |
|---|---|
| 64 bits | 64 bits |

In IPv6 all interfaces have a /64 mask. There's not subnetting in IPv6. There's no need for NAT either.

## Format

X:X:X:X:X:X:X:X     where X = 16 bit Hexadecimal field

E.g.
2001:0000:13Of:0000:0000:09d0:876a:123B

**Format Rules**
- Leading zeros are optional
- Succesive fields of zeros can be represented as ::
	- But only once per address

Following these rules, we could write the example above as follows:

2001:0:130f::09d0876a:123B

## URLs
When using IPv6 on a Web Browser, you need to enclose the IPv6 address in square brackets.
E.g.
https:// \[2001:123:4567::8\]:8080/index.html



Case insensitive

## IPv6 Unicast Addresses

### Unspecified
	::/128

### Loopback
	::1/128

### Aggregate Global
	2001::/16
	2002::/16
	3FFE3::/16
	(There's no need for NAT with IPv6)

### Unique local
This are private addresses which cannot be used over the internet.
Address block `FC::` to `FDFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF`
A later update requires the 8th bit to be set to 1, so the first two digits must be FD.
e.i.
`FD45:93AC:8A8F:0001:0000:0000:0000:0001/64`

FD -> unique local address indicator
45:93AC:8A8F -> 40bit global ID which should be randomly generated
0001 -> 16-bit subnet identifier
0000:0000:0000:0001 -> 64-bit interface identifier (the host portion of the address)

### Link Local
Address block   `FE80::/10`  (`FE80:: to FEBF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF`)
However, the standard states that the 54 bits after FE80/10 should all be 0, so the resulting block will always start with `FE80`

The interface ID is generated using EUI-64 rules

These addresses are used for communication within a single link (subnet). Routers will not route packets with a link-local destination IPv6 address.

Common uses of link local addresses:
- routing protocol peerings (OSPFv3 uses link-local addresses for neighbour adjacencies)
- next-hop address for static routes
- Neighbour Discovery Protocol (NDP, IPv6's replacement for ARP) uses link-local addresses to function

### Site Local
	FEC0::/10
	LAN scope. No routable on the internet (Deprecated)

### IPv4 Compatible
	0:0:0:0:0:0::/96
	(Deprecated)

### IPv6 EUI addresses
All Aggregate Global IP addresses have a Network Prefix of 64.

| Network Prefix | Interface Identifier |
|---|---|
| 64 bits | 64 bits |

The interface ID can use Modified EUI-64 format
E.g.
![[Screenshot 2023-02-20 at 18.15.27.png]]

![[Screenshot 2023-02-20 at 18.31.22.png]]





## IPv6 Multicast Addresses
IPv6 doesn't use broadcast. 

Address range:
`FF00/8` (`FF00:: to FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF:FFFF`)


| Purpose | IPv6 Address | IPv4 Address |
|---|---|---|
| All nodes/hosts<br> (functions like broadcast) | FF02::1 | 224.0.0.1 |
| All routers | FF02::2 | 224.0.0.2 |
| All OSPF routers | FF02::5 | 224.0.0.5 |
| All OSPF DRs/BDRs | FF02::6 | 224.0.0.6 |
| All RIP routers | FF02::9 | 224.0.0.9 |
| All EIGRP routers | FF02::A | 224.0.0.10 | 

### IPv6 Multicast scopes
#### Interface-local (FF01)
The packet doesn't leave the local device. Can be used to send traffic to a service within the local device.
#### Link-local (FF02)
The packet remains in the local subnet. Routers will not route the packet between subnets.
#### Site-local (FF05)
The packet can be forwarded by routers. Should be limited to a single physical location (not forwarded over a WAN)
#### Organization-local (FF08)
Wider in scope than site-local (and entire company/organization)
#### Global (FF08)
No boundaries. Possible to be routed over the internet.


### IPv6 Routing types
- Static
- RIPng (RFC 2080)
- OSPFv3 (RFC 2740)
- IS-IS for IPv6
- MP-BGP4 (RFC 2545/2858)
- EIGRP for IPv6

In CISCO routers, you need to run `ipv6 unicast-routing` before you can configure any routing protocol.

