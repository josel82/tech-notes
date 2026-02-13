# IPV6 Configuration
#CISCO #Networking 


## Enable IPv6

```
ipv6 unicast-routing
```


## Link-local IPv6 addresses
Are automatically generated on IPv6-enabled interfaces. Use the following command, to enable IPv6 on an interface:
```
R1(config-if)#ipv6 enable
```


## Stateless DHCP configuration
### Define the DHCP Pool (Used only for DNS/Domain)
```
ipv6 dhcp pool LAN_CLIENTS
 dns-server 2001:4860:4860::8888
 domain-name lab.internal
```

### Configure the interface
```
interface Vlan10
 description VLAN_A
 ipv6 address 2001:DB8:A:1::1/64
 ipv6 address FDAC:1234:5678:1::1/64
 ipv6 dhcp server LAN_CLIENTS
 # The 'Other' flag tells clients to use DHCP for DNS
 ipv6 nd other-config-flag
 # Ensure the 'Autonomous' flag is active for all prefixes
 ipv6 nd prefix default
```
