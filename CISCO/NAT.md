#### Definitions

- **Inside Local** 
	IP address of the host as seen from the Local Network
- **Outside Local**
	IP address of the host as seen on the Internet
- **Outside Global**
	IP address of an outside host as seen on the internet
- **Inside Global**
	IP address of an outside host as seen in the Local Network

#### NAT Types

- Static
- Dynamic
- PAT (Port Address Translation | Overloading)


#### Static NAT
Implemented in cases where we want to map a host in the inside network to a static public address in the outside network. e.g. Web server with a static public IP address.

```cisco
Router#conf t
Router(config)#int f0/0
Router(config-if)#ip add 10.1.1.1 255.255.255.0
Router(config-if)#ip nat inside
Router(config-if)#no shut
Router(config-if)#int f0/1
Router(config-if)#ip add 5.5.5.1 255.255.255.0
Router(config-if)#ip nat outside
Router(config-if)#no shut
Router(config-if)#exit
Router(config)#ip nat inside source static 10.1.1.100 5.5.5.8
Router(config)#end
```

| `ip nat` | `inside` | `source` | `static 10.1.1.100` | `99.10.120.30` |
|---|---|---|---|---|
| command | place | mode | inside local address | inside global address |

Enable ip nat on the inside network, translate the source address of host (10.1.1.100) to address (99.10.120.30)

**Ambiguous translations.** Add the key work "extendable" at the end of the statement

CASE 1: One Inside Local - Many Inside Global
```cisco
Router(config)#ip nat inside source static tcp 10.1.1.100 53 5.5.5.8 53 extendable
Router(config)#ip nat inside source static tcp 10.1.1.100 80 5.5.5.10 80 extendable
```

CASE 2: Many Inside Local - One Inside Global
```cisco
Router(config)#ip nat inside source static tcp 10.1.1.100 21 5.5.5.8 13423 extendable
Router(config)#ip nat inside source static tcp 10.1.1.101 21 5.5.5.8 15200 extendable
Router(config)#ip nat inside source static tcp 10.1.1.103 21 5.5.5.8 12350 extendable
```

CASE 3: Many Inside Local - Many Inside Global
```cisco
Router(config)#ip nat inside source static 10.1.1.100 5.5.5.8 extendable
Router(config)#ip nat inside source static 10.1.1.101 5.5.5.9 extendable
Router(config)#ip nat inside source static 10.1.1.103 5.5.5.10 extendable
```

#### Dynamic NAT
We use dynamic NAT when we want to map a group of hosts in the inside network to a pool of public (inside global) addresses. Here the first host trying to connect to the internet gets the first inside local IP in the pool and the second host trying to connect gets the second IP in the pool and so forth. The mapping is removed when the communication ends.

```cisco
Router(config)#int f0/0
Router(config-if)#ip add 10.1.1.1 255.255.255.0
Router(config-if)#ip nat inside
Router(config-if)#no shut
Router(config-if)#int f0/1
Router(config-if)#ip add 5.5.5.1 255.255.255.0
Router(config-if)#ip nat outside
Router(config-if)#no shut
Router(config-if)#exit
Router(config)#access-list 1 permit 10.1.1.0 0.0.0.255
Router(config)#ip nat pool GLOB_INS 5.5.5.5 5.5.5.10 netmask 255.255.255.0
Router(config)#ip nat inside source list 1 pool GLOB_INS
Router(config)#end
```


#### PAT (Port Address Translation | Overloading)
This mode is used when we one to map all internal hosts to only one external (Outside Local) address, the router's public IP address. This is what home routers do.

```cisco
Router(config)#int f0/0
Router(config-if)#ip add 10.1.1.1 255.255.255.0
Router(config-if)#ip nat inside
Router(config-if)#no shut
Router(config-if)#int f0/1
Router(config-if)#ip add 5.5.5.1 255.255.255.0
Router(config-if)#ip nat outside
Router(config-if)#no shut
Router(config-if)#exit
Router(config)#access-list 1 permit 10.1.1.0 0.0.0.255
Router(config)#ip nat inside source list 1 interface FastEthernet 0/1 overload
```





#### Show commands
```cisco
Router#show ip nat statistics
Router#show ip nat translations
Router#show ip nat translations verbose
```

Clearing translations
```
Router#clear ip nat translations
```

In this example we want to connect a router "CiscoIOSv15.6(1)T-1" to a network that has access to the internet, and we also want devices behind this router to have access to the internet through this router.

![[NAT example.png]]

1. Enable dhcp on the interface that faces the outside network. This way the interface will get an IP address from the dhcp server in that network, thus avoiding any possible addressing conflicts.
	```cisco
	R1(config)#int g0/0 
	R1(config-if)#ip add dhcp
	R1(config-if)#no shut
	R1(config-if)#exit
	```
2. Configure NAT on the router
```cisco
	R1(config)#int g0/0
	R1(config-if)#ip nat outside
	R1(config-if)#int g0/1
	R1(config-if)#ip add 10.1.1.1 255.255.255.0
	R1(config-if)#ip nat inside
	R1(config-if)#no shut
	R1(config-if)#exit
	R1(config)#ip nat inside source list 1 interface gigabitEthernet 0/0 overload
	R1(config)#access-list 1 permit any
	R1(config)#end
```

3. Verify
	Configure the network interface on the client devices. Make sure they have an appropiate IP address set for DNS. Try pinging a web server. 
```bash
root@UbuntuDockerGuest-1:~# ping www.google.ie
PING www.google.ie (216.239.38.120) 56(84) bytes of data.
64 bytes from any-in-2678.1e100.net (216.239.38.120): icmp_seq=1 ttl=114 time=29.1 ms
64 bytes from any-in-2678.1e100.net (216.239.38.120): icmp_seq=2 ttl=114 time=24.8 ms
64 bytes from any-in-2678.1e100.net (216.239.38.120): icmp_seq=3 ttl=114 time=27.4 ms
64 bytes from any-in-2678.1e100.net (216.239.38.120): icmp_seq=4 ttl=114 time=26.7 ms
```