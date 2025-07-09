# Gathering Network info

## networksetup
The command-line tool `networksetup` is used to configure a client’s network settings.

### listallnetworkservices
Displays a list of all the network services on the computer’s hardware ports. An asterisk (*) denotes that a network service is disabled.
```
networksetup -listallnetworkservices
```

E.g
```
username@hostname ~ % networksetup -listallnetworkservices
An asterisk (*) denotes that a network service is disabled.
USB 10/100 LAN
AX88179A
Wi-Fi
Thunderbolt Bridge
VPN
```

### getinfo
Display information about a specific network service
```
networksetup -getinfo <network service>
```

E.g.
```
username@hostname ~ % networksetup -getinfo Wi-Fi
DHCP Configuration
IP address: 172.16.11.31
Subnet mask: 255.255.255.0
Router: 172.16.11.1
Client ID: 
IPv6: Automatic
IPv6 IP address: none
IPv6 Router: none
Wi-Fi ID: ad:fe:44:23:ff:45
```


### getdnsservers
Lists DNS IP addresses configured for a specific network service

```
networksetup -getdnsservers <network service>
```

## Get Local IP address
```bash
ipconfig getifaddr en0
```
## netstat

The following command lists the hosts routing table:
```
sudo netstat -rn
```

better to run this command as a super user
