# Network basic commands
#Linux #Debian #Networking 


## Changing interface's IP address
```bash
ifconfig <iface> <ip add>
```
E.g.
```
ifocnfig eth0 192.168.180.160
```

## Changing interface's subnet mask and broadcast address
```
ifconfig eth0 192.168.180.160 netmask 255.255.0.0 broadcast 192.168.255.255
```

## Changing interface's MAC Address
```
ifconfig eth0 down
ifconfig eth0 hw ether aa:bb:cc:dd:ee:ff
ifocnfig eth0 up
```


## Configuring interface to obtain an IP address from a DHCP server
```
dhcpclient <iface>
```
E.g.
```
dhcpclient eth0
```

## DNS queries
Find the name servers for a particular domain. Here the `ns` option stands for name server
```
dig my-domain.com ns 
```

Find email servers connected to a particular domain
```
dig my-domain.com mx
```

## Find your public IP address from the CLI
```
curl ifconfig.me
```