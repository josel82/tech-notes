### Static Routing

	Routes are set manually by the administrator.

### Dynamic Routing Protocol
-   Distance Vector Protocol
-   RIPv2
-   Link State
-   OSPF 
-   EIGRP
-   IS-IS

| | Advantages | Disadvantages |
|---|---|---|
| static | Less overhead | Not scalable |
| Dynamic | Ideal for big networks | Uses Processing power and network resources |

AS = Autonomous System
        Group of routers managed by a single administrator
IGP = Interior Gateway Protocol
		Routing protocols used within an autonomous system. e.g. RIPv2, OSPF, EIGR, IS-IS
BGP = Border Gateway Protocol
		Routing protocol used for routing across different autonomous systems

### Useful commands

- `router#sh ip protocol`
- `router#sh ip chef`

- `router#debug ip packet`   
  `{Warning... no recommended for use in production networks}`
- `router#debug ip icmp`
- `router#un all`

- `router#ping <dest IP> <src interface>` 
specifies the source interface for the ping

- `router(config)#ip domain-lookup`
- `router(config)#ip name-server <DNS IP address>`


### Gateway of last resort

#### static default route
`router(config)#ip route 0.0.0.0 0.0.0.0 <router IP>`     

use when ip routing is enabled / in devices that forward
packets for other devices e.g. Routers and Multilayer Switches with ip routing enabled

If you set up two or more static default routes of the same cost, the router would load balance
the packets between the two routes

If you set up two or more static default routes of different costs, the router would chose
the path of less cost as the default route and the others would be used as back up paths

in case the lower cost path fails.

### Default Gateway

`router(config)#ip default-gateway <router IP>`          

use when ip routing is disabled / end devices or layer 2
devices e.g. PCs, Layer 2 Switches

### How to delete static routes
`router(config)#no ip route <dest network ip> <mac add> <next hop ip>`

### Setup switch vlan interface to get ip address through DHCP

`S1(config)#int vlan 1`
`S1(config-if)#ip add dhcp`