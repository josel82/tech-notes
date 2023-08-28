# Dynamic ARP Inspection (DAI)
#CISCO #CyberSecurity #EthicalHacking 

Dynamic ARP Inspection (DAI) is a security feature that validates Address Resolution Protocol (ARP) packets in a network. DAI allows a network administrator to intercept, log, and discard ARP packets with invalid MAC address to IP address bindings. This capability protects the network from certain “man-in-the-middle” attacks [1](https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst4500/12-2/25ew/configuration/guide/conf/dynarp.html). DAI inspects ARPs on the LAN and uses the information in the DHCP snooping database on the switch to validate ARP packets and to protect against ARP spoofing [2](https://www.juniper.net/documentation/us/en/software/junos/security-services/topics/topic-map/understanding-and-using-dai.html)[3](https://documentation.meraki.com/MS/Other_Topics/Dynamic_ARP_Inspection).

## Enable DAI globally
```cisco
conf t
ip arp inspection vlan 1
ip arp inspection validate src-mac
```

## Trust a given port
```cisco
int g0/0
ip arp inspection trust
exit
```

NOTE: DAI relies on DHCP Snooping binding table on the switch. If you encounter problems after enabling DAI and setting up trusted port, check the DHCP Snooping binding table [[DHCP Snooping#^d84648]]; If there are no entries, try to renew the DHCP lease on the client PC.

## Show commands
```cisco
show ip arp inspection
```