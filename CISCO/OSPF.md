
(Open Shortest Path First)
It uses the Shortest Path First algorithm

It's a Link State Running Protocol

Link - router Interface
State - description of an inerface and its relationship to neighbours routers

A collection of link state for a topological database or link state database

Sends hello packets to multicast IP address 254.0.0.5 

#### Configuration
```
#Going into configuration mode
Router#conf t

#Enable OSPF with process ID 1 (This number is local to the router)
Router(config)#router ospf 1

#Add interface to area 0
Router(config-router)#network 10.1.1.1 0.0.0.0 area 0

#Add all interfaces to area 0
Router(config-router)#network 0.0.0.0 255.255.255.255 area 0

#or 

#Add a network segment to area 0
Router(config-router)#network 10.1.2.1 0.0.0.255 area 0

#or

#Assign router ID (convention is to match the ID number with loopback interface address)
Router(config-router)#router-id 1.1.1.1

```

Here is another way to configure OSPF. This time we are going to use the interface command.

```cisco
Router#conf t
Router(config)#router ospf 1
Router(config-router)#int g0/0
Router(config-if)#ip ospf 1 area 0
Router(config-if)#int g0/1
Router(config-if)#ip ospf 1 area 0
```

#### Priority
The router with the higher priority becomes the Designated Router on a network segment. Priority 0 makes a router not elegible for DR or BDR. The router with the second higher priority becomes the BDR (Backup Designated Router). The rest become DROTHER
```cisco
#Go to the interface connected to the network segment in which you want the router to become the DR
Router(config)#int g0/0

#Then set the priority to a number that would make it the DR
Router(config-if)#ip ospf priority 10
```

#### Autonomous System Border Router (ASBR) Router Ridistribution
It is a router that has interfaces in different Autonomous Systems. In this example R2 has g0/0 int EIGRP 100 and g0/1 in OSPF 1.

![[Screenshot 2023-02-08 at 18.00.08.png]]

```cisco
R2#conf t
R2(config)#int g0/0
R2(config-if)#ip add 10.1.1.2 255.255.255.0
R2(config-if)#int g0/1
R2(config-if)#ip add 10.1.2.1 255.255.255.0
R2(config-if)#int loop 0
R2(config-if)#ip add 2.2.2.2 255.255.255.0
R2(config-if)#exit
R2(config)#router eigrp 100
R2(config-router)#network 10.1.1.2 0.0.0.0
R2(config-router)#router ospf 1
R2(config-router)#network 10.1.2.1 0.0.0.0 area 1
R2(config-router)#network 2.2.2.2 0.0.0.0 area 1
R2(config-router)#redistribute eigrp 100
R2(config-router)#router eigrp 100
R2(config-router)#redistribute ospf 1 metric 10000 1000 255 1 1500

```

#### Multiarea OSPF
It is required that all areas have a border with area 0 (backbone). Intra Area Routers without an interface in Area 0, won't be able to advertise its interfaces to other areas.

The following is an example where we have an internal area (Area 2) that is not bordering Area 0
![[Screenshot 2023-02-08 at 17.37.51.png]]

Is it is, R5 interfaces won't be advertised to other areas. This particular case can be fixed by creating virtual interfaces in R2 and R4, creatin a tunnel through Area 1 in order to connect Area 2 to Area 0. 

command: 

| Area we want to travers | command | Neighbour Router ID |
|---|---|---|
| `area 1` | `virtual-link` | `5.5.5.5` |

```cisco
R2(config)#router ospf 1
R2(config-router)#area 1 virtual-link 4.4.4.4
```

```cisco
R4(config)#router ospf 1
R4(config-router)#area 1 virtual-link 2.2.2.2
```

#### Show commands
```cisco
Router#show run | section ospf

Router#show ip protocol

Router#show ip ospf 

Router#show ip ospf interface

Router#show ip ospf interface brief

Router#show ip ospf neighbour

Router#show ip ospf <router-id>

Router#show ip ospf database

Router#show ip ospf database router <router-id>

```

#### Other commands
```cisco
Router#debug ip ospf events
Router#debug ip ospf adj

Router#clear ip ospf process
```

#### Troubleshooting
- Network type mismatch:
In this example lets assume that we have two routers (R1 and R2) and they form a segment with interface g0/1 on both routers. However, someone has set the network type on interface g0/1 of R2 as "non-broadcast". This will break the neighbour relationship between these two routers. This is how we can fix it: 
```cisco
R2(config)#int g0/1
R2(config-if)#ip ospf network broadcast
R2(config-if)#exit
```


#### OSPF Database

This an example of the OSPF database of a router (R1) that is in Area 1
![[Screenshot 2023-02-08 at 19.04.32.png]]

- LSA Type 1: Router Link States (Area 1)
	Lists all routers within Area 1

- LSA Type 2: Net Link States (Area 1)
	Lists the designated router for Area 1

- LSA Type 3: Summary Link States (Area 1)
	Lists all the routes originated from other areas