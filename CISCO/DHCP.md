### DHCP Server Setup

1.   exclude addresses
	`router(config)#ip dhcp excluded-addresses [IP address|IP address range]`

2.   create a pool of addresses
	`router(config)#ip dhcp pool [name]`

3.   define network
	`router(dhcp-config)#network [IP address] [Subnet Mask]`

4.   specify default gateway
	`router(dhcp-config)#default-router [IP address]`

5.   specify DNS
	`router(dhcp-config)#dns-server [IP address]`

6.   setup lease time
	`router(dhcp-config)#lease [days]`

7.   configure domain name (Optional)
	`router(dhcp-config)#domain-name example.com`

8.   configure TFTP for IP phones (Optional)
	`router(dhcp-config)#option 150 ip [TFTP server/CISCO unified communications manager IP address]`


### Some show commands

- #### On the server
  `router#sh ip dhcp binding`
  `router#sh ip dhcp pool [name]`
  `router#sh ip dhcp server statistics`

- #### On the client
  `client#sh dhcp lease`

### Miscellaneous

- #### How to change an interface's mac address
  `client(config-if)#mac-address aaaa.bbbb.cccc`

- #### How to configure an interface so it gets IP address via DHCP
  `client(config-if)#ip address dhcp`

- #### How to change the client-id
  `client(config-if)#ip dhcp client client-id ascii <string>`

- #### How to forward DHCP discover packets to a DHCP server in another network
  `router2(config)#int g0/0     => interface on the client's network`
  `router2(config-if)#ip helper-address <DHCP server's IP address>`

	Discover messages are sent from the client device to the broadcast
	IP address, and because routers drop broadcast packets, we need to
	do this step in other to forward these messages to a DHCP server
	located in a network located on the other side of the router


### Debugging

- #### at the DHCP server
	`router#debug ip dhcp server packet`