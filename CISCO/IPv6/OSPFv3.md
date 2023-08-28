Follow these steps in order to enable OSPFv3 on cisco routers
1. Enable IPv6 routing
```cisco
R1(config)#ipv6 unicast-routing
```
2. Configure OSPF proccess
```cisco
R1(config)#ipv6 router ospf 1
```
3. Set router ID
```
R1(config-rtr)#router-id 1.1.1.1
R1(config-rtr)#exit
```
4. Configure interface
```cisco
R1(config)#int g0/1
R1(config-if)#ipv6 address 2001:1::1/64
R1(config-if)#no shut
```
5. enable OSPF on the interface
```cisco
R1(config-if)#ipv6 ospf 1 area 0
R1(config-if)#end
```


#### How to set up OSPFv3 without an IPv6 Global Unicast address
```cisco
R1#conf t
R1(config)#ipv6 unicast-routing
R1(config)#ipv6 ospf 1
R1(config-rtr)#router-id 1.1.1.1
R1(config-rtr)#exit
R1(config)#int g0/0
R1(config-if)#ipv6 enable
R1(config-if)#ipv6 ospf 1 area 0
```
In this case OSPF uses the routers Link-Local address to establish neighbour relationships with other roters


#### Show commands:
```cisco
show ipv6 route
show ipv6 ospf
show ipv6 ospf interface brief
show ipv6 ospf neighbour
```

#### Passive interfaces
These will break the neighbour relationships with other OSPF routers
```
R1(config)#ipv6 ospf 1
R1(config-rtr)#passive-interface default
```
Enable passive interface on only one interface
```
R1(config)#ipv6 ospf 1
R1(config-rtr)#passive-interface g0/0
```