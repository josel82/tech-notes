1.  On the switch, configure the interface connected to the router as a trunk interface
		`Switch(config-if)#switchport trunk encapsulation dot1Q`
		`Switch(config-if)#switchport mode trunk`
		`Switch(config-if)#end`

2.  Create vlans
		`Switch(config)#vlan 2`
		`Switch(config-vlan)#vlan 3`
		`Switch(config-vlan)#exit`

3.  Add ports to each vlan
		`Switch(config)#int f0/2`
		`Switch(config-if)#switchport mode access`
		`Switch(config-if)#switchport access vlan 2`
		`Switch(config-if)#int f0/3`
		`Switch(config-if)#switchport mode access`
		`Switch(config-if)#switchport access vlan 3`
		`Switch(config-if)#end`

4.  Configure trunk port
		`Switch(config)#int f0/1`
		`Switch(config-if)#switchport mode trunk`
		`Switch(config-if)#switchport trunk encapsulation dot1Q`
		`Switch(config-if)#switchport nonegociate`

5.  On the router, configure the interface connected to the switch as follows
		`Router(config)#int g0/0`
		`Router(config-if)# no shut`

6.  Then set up sub interfaces, one per vlan
		`Router(config-if)#int g0/0.1`
		`Router(config-subif)#encapsulation dot1Q 1 native`
		`Router(config-subif)#ip add 192.168.1.1 255.255.255.0`
		`Router(config-subif)#no shut`
		`Router(config-if)#int g0/0.2`
		`Router(config-subif)#encapsulation dot1Q 2`
		`Router(config-subif)#ip add 192.168.2.1 255.255.255.0`
		`Router(config-subif)#no shut`
		`Router(config-if)#int g0/0.3`
		`Router(config-subif)#encapsulation dot1Q 3`
		`Router(config-subif)#ip add 192.168.3.1 255.255.255.0`
		`Router(config-subif)#no shut`