# Network Settings in Ubuntu Server
#Linux #Interfaces

[Documentation](https://ubuntu.com/server/docs/network-configuration)

## Identify interface
```bash
ip addr
```

or
```bash
sudo lshw -class network
```

## Temporary IP address assignment
```bash
sudo ip addr add 10.1.1.10/24 dev ens18 
```

## Set link Up/Down
```bash
ip link set dev enp0s25 up
ip link set dev enp0s25 down
```

### Verify IP address configuration
```bash
ip address show dev enp0s25
```

## Set Default Gateway
```bash
sudo ip route add default via 10.1.1.1
```

### Verify Default Gateway configuration
```bash
ip route show
```
or
```bash
route -n
```

## Get DNS servers information
```bash
systemd-resolve --status
```

## Set DNS servers
`/etc/resolv.conf`
```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

## Clear interface configuration
```bash
ip addr flush eth0
```


## Configuring Static IP Address

^035879

1. Search for existing Netplan config file
```bash
ls -l /etc/netplan
```

2. This file might be named differently on your server. Before editing the config file we are going to create a backup file we can revert to in case there is an issue.
```bash
sudo cp /etc/netplan/config.yaml /etc/netplan/config.yam.bkp
```

3. Open Netplan's config file with your text editor of choice. 
```bash
sudo nano /etc/netplan/config.yaml
```

4. Edit the file as follows
```yaml
network:
  version: 2
  ethernets:
    en0:
	    addresses: [192.168.0.25/24]
	    nameservers:
	        addresses: [8.8.8.8, 1.1.1.1]
		routes:
			- to: default
			  via: 192.168.0.1
```
Save and close the file.

5. Test the configuration
```bash
sudo netplan try
```

6. Apply the configuration:
```bash
sudo netplan apply
```

## Release DHCP lease
```bash
sudo dhclient -v -r
```

## Obtain an IP address via DHCP
```bash
sudo dhclient -v
```

## Dynamic IP address assignment (DHCP Client)

1. Open Netplan's config file. This file might be named differently on your server.
```
sudo nano /etc/netplan/config.yaml
```

2. Edit the file as follows:
```yaml
network:
   version: 2
   renderer: networkd
   ethernets:
     enp3s0:
        dhcp4: true
```
Save and close the file.

3. Apply the configuration:
```bash
sudo netplan apply
```

## How to disable IPv6
https://linuxconfig.org/how-to-disable-ipv6-address-on-ubuntu-22-04-lts-jammy-jellyfish
