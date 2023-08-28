#### Create a VLAN
`switch>enable
`switch#conf t
`switch(config)#vlan 10`

#### Setup port as an access port for a VLAN
`switch(config)#int f0/1`
`switch(config-if)#switchport mode access`
`switch(config-if)#switchport access vlan 10`
`switch(config-if)#no shutdown`
`switch(config-if)#exit

#### Setup port as a trunk port
`switch(config)#int g1/0/1`
`switch(config-if)#switchport mode trunk`

`or`

`switch(config-if)#switchport encapsulation dot1q`
`switch(config-if)#switchport mode trunk`
`(depending on the switch)`

#### Configure VLAN interface
`switch(config)#int vlan 1`
`switch(config-if)#ip add 10.1.1.1 255.255.255.0`
`switch(config-if)#no shutdown`
`switch(config-if)#exit`

#### Define a default gateway
`switch(config)#ip default-gateway 10.1.1.254`

#### How to enable IP routing in a L3 switch
`switch(config)#ip routing`

#### How to forward VLAN packets to router
`switch(config)#int vlan10`
`switch(config-if)#ip helper-address 10.1.1.254`
`switch(config-if)#exit`
	at the router you need to configure static routes for such vlan

#### Some "show" commands
`switch#sh vlan`
`switch#sh vlan brief`
`switch#sh int f0/1 switchport`
`switch#sh int f0/1 status`

#### Configure VTP
at the core switch
`switch(config)#vtp domain ccna`
`switch#sh vtp status`

at the access switch
`switch(config)#vtp domain ccna`
`(for packet tracer. In the real world this command isn't necessary)`
`switch(config)#vtp mode client`

setup password
`switch(config)#vtp password cisco`

mode transparent
`switch(config)#vtp mode transparent`