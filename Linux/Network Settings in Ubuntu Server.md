# Network Settings in Ubuntu Server
#Linux #Interfaces

[Documentation](https://ubuntu.com/server/docs/network-configuration)

## Identify interface
```bash
ip a
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
1. Search for existing Netplan config file
```bash
ls -l /etc/netplan
```

2. Open Netplan's config file with your text editor of choice. This file might be named differently on your server.
```bash
sudo nano /etc/netplan/config.yaml
```

3. Edit the file accordingly
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    en0:
      dhcp4: no
      addresses:
        - 192.168.0.25/24
      gateway4: 192.168.0.1
      nameservers:
          addresses: [8.8.8.8, 1.1.1.1]
```
Save and close the file.

Apply the configuration:
```bash
sudo netplan apply
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



