# How to set up bridge interface on Proxmox VM
#GNS3 #Proxmox 

[Source->](https://www.youtube.com/watch?v=7m77QAlwy1o)

1. Log in to the VMs shell
2. Update and upgrade packet libraries
```bash
sudo apt update -y
```

```bash
sudo apt upgrade -y
```

3. Install bridge-utils packet
```bash
sudo apt install bridge-utils -y
```

4. Configure bridge interface
First, backup netplan yaml file:
```bash
sudo cp /etc/netplan/00-installer-config.yaml /etc/netplan/00-installer-config.yaml.bak
```

Edit netplan yaml file:
```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

[source:](https://github.com/Jamous/RN_config_files/tree/main/gns3_bridge)

There are two options. Pick the one that applies to your set up:
DHCP
```yaml
network:
  ethernets:
	ens18:
	  dhcp4: true
	ens19:
	  dhcp4: false
	  dhcp6: false
version: 2

bridges:
  br0:
	interfaces: [ens19]
	  dhcp4: no
	  dhcp6: no
```

Static
```yaml
network:
  ethernets:
    ens18:
      addresses:
      - 10.0.1.4/23
      gateway4: 10.0.0.1
      nameservers:
        addresses:
        - 10.0.0.1
        search:
        - mylilserver.net
    ens19:
      dhcp4: false
      dhcp6: false
version: 2

bridges:
  br0:
    interfaces: [ens19]
      dhcp4: no
      dhcp6: no
```

5. Once you have edited the config file, you can apply the changes
```bash
sudo netplan apply
```
