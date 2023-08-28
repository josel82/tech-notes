CISCO formats mac addresses as follows
`aaaa.bbbb.cccc`

other vendors may format them differently
`AA.BB.CC.DD.EE.FF   Windows`
`aa:bb:cc:dd:ee:ff   Linux`

Switches forget mac addresses after 5 minutes if a device doesn't communicate in that period of time.

## COMMANDS

`Switch#sh mac address-table`                 
shows all mac addresses even default mac addresses that aren't useful for this purposes

``Switch##sh mac address-table dynamic`              
shows only mac addresses that have been learned (this is what we want to see)

`Switch#sh mac address-table dynamic | include aaaa.bbbb.cccc`
This command will filter the previous command by the provided mac address

`Switch#sh mac address-table interface f0/1`  
Shows all mac addresses that have been learned from a specific interface. Many mac addresses linked to one interface indicates that chances are that the device connected to it is a switch or a wireless access point.

`Switch#sh mac address-table address aaaa.bbbb.cccc`
Shows the interface where a specific mac address have been learned from.

## USEFUL COMMANDS

`Switch#sh cdp neighbours    <Only CISCO devices>`
or
`Switch#sh lldp neighbours   <industry standard>`
Provides information about directly connected devices. this command is very useful to layout a network we don't have much information about.

`Switch#sh cdp neighbours detail`
Shows more information, such as IP addresses and more.

******************************************************************************************

`Switch#sh arp`
Provides a table that matches IP addresses with IP addresses. Particularly useful when looking for a device by only its IP address.

## IMPORTANT
Do this after pinging the device in question to make sure that first, the device is in the network and second, that the IP address is learned in the arp cache.

******************************************************************************************

`usename@laptop~$ nslookup     (From command prompt or Terminal)`
This command will query the DNS server for the IP address of a device by providing its domain name.