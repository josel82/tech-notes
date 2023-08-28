#### Static Routes

In the following example we have two routers (R1 & R2) which have loopback interfaces configured as shown in the picture below. In order to be able to ping eachother's loopbacks, each router would need a route for that IP address:

![[Screenshot 2023-02-23 at 20.35.11.png]]

```cisco
R1#conf t
R1(config)#ipv6 unicast-routing
R1(config)#int s0/0/0
R1(config-if)#ipv6 address 2001:1::1/64
R1(config-if)#no shut
R1(config-if)#exit
R1(config)#ipv6 route 2001:FACE:2::1/64 int s0/0/0
```

```cisco
R2#conf t
R2(config)#ipv6 unicast-routing
R2(config)#int s0/0/0
R2(config-if)#ipv6 address 2001:1::2/64
R2(config-if)#no shut
R2(config-if)#exit
R2(config)#ipv6 route 2001:FACE:1::1/64 int s0/0/0
```

**Notice** that here we have used the Local Outgoing Interface in the static route command instead of the next hope. This works well in point to point links, such as this, but it doesn't work on Ethernet links. For those cases use the next hope IP address.




#### Routing Protocols
- RIPng (RIP next generation)
- OSPFv3
- IS-IS for IPv6
- MP-BGP4
- EIGRP for IPv6

Before we can configure IPv6 routing on a CISCO router we must run:
```cisco
Router(config)#ipv6 unicast-routing
```


#### RIPng
```cisco
R1#conf t
R1(config)#ipv6 unicast-routing
R1(config)#ipv6 router rip RIPNG1
R1(config-rtr)#int f0/0
R1(config-if)#ipv6 rip RIPNG1 enable
R1(config-if)#int f0/1
R1(config-if)#ipv6 rip RIPNG1 enable
R1(config-if)#end
R1#show ipv6 route
```

You can advertise a default route from one router to another as follows:
```cisco
R1(config)#int f0/1
R1(config-if)#ipv6 rip RIPNG1 default-information originate
```

RIPng show commads
```cisco
show ipv6 rip
show ipv6 route rip
```


#### OSPF
```cisco
R1#conf t
R1(config)#ipv6 router ospf 1
R1(config-rtr)#router-id 1.1.1.1
R1(config-rtr)#int f0/1
R1(config-if)#ipv6 ospf 1 area 0
R1(config-if)#int f0/0
R1(config-if)#ipv6 ospf 1 area 1
R1(config-if)#end
R1#show ipv6 route
```

Clear the OSPF process like so:
```cisco
R1#clear ipv6 ospf process
```

#### IPv6 tunnel over IPv4

![[Screenshot 2023-02-21 at 16.50.58.png]]

```cisco
R1(config)#int tun 0
R1(config-if)#ipv6 address 2003::1/64
R1(config-if)#tunnel source 10.1.2.1
R1(config-if)#tunnel destination 10.1.2.2
R1(config-if)#tunnel mode ipv6ip
R1(config-if)#exit
R1(config)#ipv6 route 2001:1:1:3::/64 tun 0
```

```cisco
R2(config)#int tun 0
R2(config-if)#ipv6 address 2003::2/64
R2(config-if)#tunnel source 10.1.2.2
R2(config-if)#tunnel destination 10.1.2.2
R2(config-if)#tunnel mode ipv6ip
R2(config-if)#exit
R2(config)#ipv6 route 2001:1:1:1::/64 tun 0
```

================================================================
Static:
```cisco
Router#conf t
Router(config)#ipv6 unicast-routing
Router(config)#int g0/0
Router(config-if)#ipv6 address 2001:1:1:1::1/64
Router(config-if)#no shut
```

EUI-64
```cisco
Router(config)#int g0/0
Router(config-if)#ipv6 address 2001:2::/64 eui-64
Router(config-if)#no shut
```

Show commands
`Router#sh ipv6 int f0/0`