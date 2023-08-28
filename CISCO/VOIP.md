#### (IMPORTANT)
IP Phones use CDP/LLDP for communication with the switch. You need to enable CDP or LLDP on the switch when working with IP phones.
`switch(config)#cdp run`

#### Connecting phones and PCs to a trunk port
Configure the port you are connecting both the phone and PC as trunk, then prune the trunk by allowing only the default vlans along with the voice vlan, this way we avoid issues caused by too many broadcast packets from different vlans arriving at the phone.

```cisco
switch#conf t
switch<config>#int f0/1/1
switch<config-if>#switchport trunk encapsulation dot1q
switch<config-if>#switchport mode trunk
switch<config-if>#switchport trunk native vlan 1
switch<config-if>#switchport voice vlan 2
switch<config-if>#switchport trunk allowed vlan 1,2,1002-1005
switch<config-if>#end
```

#### Multi-Vlan Access Port
In this approach, we configure the switch port as an access port with two vlans (Native & Voice)
```cisco
switch#conf t
switch<config>#int f0/1/1
switch<config-if>#switchport mode access
switch<config-if>#switchport voice vlan 2
switch<config-if>#switchport access vlan 1
switch<config-if>#end
```

#### Single Vlan Access port
In this implementation both the phone and the PC reside in the same vlan and the switch port they are connected to is set as an access port and is assigned to a specific vlan. The phone uses 802.1Q tags with priority bits or COS set to 5 to indicate to the switch that it is sending voice packets and QoS can be applied accordingly. The phone set the VLAN value of the 802.1Q tag to 0 in order to send tagged packets to an access port.
```cisco
switch#conf t
switch<config>#int f0/1/1
switch<config-if>#switchport mode access
switch<config-if>#switchport voice dot1p
switch<config-if>#switchport access vlan 2
switch<config-if>#end
```



#### Show commands
```
switch#show vlan brief

switch#show vlan-switch

switch#show run int f0/1/1

switch#show int f0/1/1 switchport

switch#show power inline

switch#show cdp neighbours

switch#show ephone
```