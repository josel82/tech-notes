# VLANs
#CISCO #Networking #IT 

## Create a VLAN
`switch>enable
`switch#conf t
`switch(config)#vlan 10`

## Setup port as an access port for a VLAN
```
switch(config)#vlan 10
switch(config)#int f0/1
switch(config-if)#switchport mode access
switch(config-if)#switchport access vlan 10
switch(config-if)#no shutdown
switch(config-if)#exit
```

## Configure a voice VLAN
Voice VLANs use the same access ports as Access VLANs. The idea is to have a PC and an IP phone connected to the same switch port.
```
switch(config)#vlan 10
switch(config)#vlan 11
switch(config)#int f0/1
switch(config-if)#switchport mode access
switch(config-if)#switchport access vlan 10
switch(config-if)#switchport voice vlan 11
switch(config-if)#end
```

## Setup port as a trunk port
```
switch(config)#int g1/0/1
switch(config-if)#switchport mode trunk
```

Switches that support both 802.1Q and ISL, will negotiate a VLAN encapsulation protocol; But you can manually define it as follows:
```
switch(config-if)#switchport encapsulation dot1q
```

### Disable Dynamic Trunking Protocol (DTP) 
On interface configuration mode:
```
switch(config-if)#switchport nonegotiate
```
Be aware that Administrative modes **dynamic desirable** and **dynamic auto** require negotiation, disabling DTP on ports that are configured in either mode could cause the ports not to trunk.

## Restrict VLAN traffic in a trunk
```
SW1(config-if)#switchport trunk allowed vlan 1-10
```


## Configure VLAN interface
`switch(config)#int vlan 1`
`switch(config-if)#ip add 10.1.1.1 255.255.255.0`
`switch(config-if)#no shutdown`
`switch(config-if)#exit`

## Define a default gateway
`switch(config)#ip default-gateway 10.1.1.254`

## How to enable IP routing in a L3 switch
`switch(config)#ip routing`

## How to forward VLAN packets to router
`switch(config)#int vlan10`
`switch(config-if)#ip helper-address 10.1.1.254`
`switch(config-if)#exit`
	at the router you need to configure static routes for such vlan

## Some "show" commands
```
switch#show vlan
switch#show vlan brief
switch#show vlan id 20
switch#show vlan name MCR
switch#show vlan summary
switch#show interfaces f0/1 switchport
switch#show interfaces trunk
switch#show interfaces f0/1 trunk
switch#show interfaces f0/1 status
switch#show vtp status
```


## Configure VTP
### Mode Server
By default switches are configured in VTP Server mode
`switch(config)#vtp domain ccna`
`switch#sh vtp status`

### Mode Access
`switch(config)#vtp domain ccna`
`(for packet tracer. In the real world this command isn't necessary)`
`switch(config)#vtp mode client`

### Mode Transparent
Switch forwards VTP advertisements but does not change its VLAN database
```
switch(config)#vtp mode transparent
```

### Turn off VTP
```
switch(config)#vtp mode off
```