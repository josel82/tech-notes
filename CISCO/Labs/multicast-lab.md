# Multicast Lab

![[Screenshot 2026-01-23 at 22.36.29.png]]

## R1
```bash
conf t
ip multicast-routing
int g0/0
 ip add 192.168.20.1 255.255.255.0
 no shut
int g0/1
 ip add 172.16.1.1 255.255.255.0
 no shut
int l0
 ip add 1.1.1.1 255.255.255.255
 no shut
int range g0/0-1
 ip pim sparse-mode
 exit
ip pim rp-address 1.1.1.1
```

## Arista switch
```bash
conf t
ip igmp snooping
ip igmp snooping vlan 1
```

## S1
```bash
conf t
int g0/1
 ip add 172.16.1.2 255.255.255.0
 no shut
ip route 0.0.0.0 0.0.0.0 172.16.1.1
!
!#Generate Multicast traffic
ping 239.1.1.100 repeat 99999999
```

## H1
```bash
conf t
int g0/0
 ip add 192.168.20.101 255.255.255.0
 no shut
!#Join Multicast group
 ip igmp joing-group 239.1.1.100
!#Leave Multicast group
 no ip igmp joing-group 239.1.1.100
```

## H2
```bash
conf t
int g0/0
 ip add 192.168.20.102 255.255.255.0
 no shut
!#Join Multicast group
 ip igmp joing-group 239.1.1.100
!#Leave Multicast group
 no ip igmp joing-group 239.1.1.100
```