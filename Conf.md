
## Spine-1 

Cancel Zero Touch Provisioning
```
zerotouch cancel
```

Config:
```
enable
conf
hostname Spine-1
vlan 10
name SudioFloor
int vlan 10
ip add 10.10.0.1/24
no shut
int Et 12
no switchport
ip add dhcp
no shut
int Et 11
no switchport
ip add 10.100.0.5/30
no shut
int Et 10
no switchport
ip add 10.100.0.1/30
no shut
int Et 1
switchport mode access
switchport access vlan 10
int Et 2
switchport mode access
switchport access vlan 10
int loop 1
ip add 10.10.10.1/32
no shut
exit
ip routing
router ospf 1
router-id 10.10.10.1
network 0.0.0.0/0 area 0
exit
ip route 0.0.0.0/0 10.1.20.1
end
copy run start

```

Multicast Config
```
ip igmp snooping
ip igmp snopping vlan 10
ip igmp snooping vlan 10 querier address 10.10.0.1
ip igmp snooping vlan 10 querier
ip igmp snooping vlan 10 version 3
ip igmp snooping vlan 10 fast-leave
ip multicast-routing
int vlan 10
ip pim sparse-mode
int Et 10
ip pim sparse-mode
int Et 11
ip pim sparse-mode
exit
ip pim rp-address 10.10.10.1
end

```


## Leaf-1

```
enable
conf
hostname Leaf-1
vlan 30
name Ingest
int vlan 30
ip add 10.30.0.1/24
no shut
int Et 11
no switchport
ip add 10.100.0.6/30
no shut
int Et 1
switchport mode access
switchport access vlan 30
int loop 1
ip add 10.10.10.2/32
no shut
exit
ip routing
router ospf 1
router-id 10.10.10.2
network 0.0.0.0/0 area 0
exit
ip route 0.0.0.0/0 10.1.20.1
end
copy run start

```

Multicast Config
```
ip igmp snooping
ip igmp snopping vlan 30
ip igmp snooping vlan 30 querier address 10.30.0.1
ip igmp snooping vlan 30 querier
ip igmp snooping vlan 30 version 3
ip igmp snooping vlan 30 fast-leave
ip multicast-routing
int vlan 30
ip pim sparse-mode
int Et 11
ip pim sparse-mode
exit
ip pim rp-address 10.10.10.1
end

```
## Leaf-2

```
enable
conf
hostname Leaf-2
vlan 20
name Studio5
vlan 40
name CAR
int vlan 20
ip add 10.20.0.1/24
no shut
int vlan 40
ip add 10.40.0.1/24
no shut
int Et 10
no switchport
ip add 10.100.0.2/30
no shut
int Et 1
switchport mode access
switchport access vlan 20
int Et 2
switchport mode access
switchport access vlan 20
int Et 3
switchport mode access
switchport access vlan 40
int loop 1
ip add 10.10.10.3/32
no shut
exit
ip routing
router ospf 1
router-id 10.10.10.3
network 0.0.0.0/0 area 0
exit
ip route 0.0.0.0/0 10.1.20.1
end
copy run start
```

Multicast Config
```
ip igmp snooping
ip igmp snopping vlan 20
ip igmp snooping vlan 20 querier address 10.20.0.1
ip igmp snooping vlan 20 querier
ip igmp snooping vlan 20 version 3
ip igmp snooping vlan 20 fast-leave
ip igmp snopping vlan 40
ip igmp snooping vlan 40 querier address 10.40.0.1
ip igmp snooping vlan 40 querier
ip igmp snooping vlan 40 version 3
ip igmp snooping vlan 40 fast-leave
ip multicast-routing
int vlan 20
ip pim sparse-mode
int vlan 40
ip pim sparse-mode
int Et 10
ip pim sparse-mode
exit
ip pim rp-address 10.10.10.1
end

```