# How to create NIC bond for Link Aggregation
#Proxmox #Virtualization #Networking 

1. Aggregate ports on your switch
2. Open a terminal session on your PVE node
3. Then, open and edit `/etc/network/interfaces`
```bash
nano /etc/network/interfaces
```

 and add the following lines:
```/etc/network/interfaces
auto eno1
iface eno1 inet manual

auto eno2
iface eno2 inet manual

auto bond0
iface bond0 inet manual
		bond-slaves eno1 eno2
		bond-miimon 100
		bond-mode 802.3ad
		bond-xmit-hash-policy layer3+4
```

Now add a new bridge config
```etc/network/interfaces
auto eno1
iface eno1 inet manual

auto eno2
iface eno2 inet manual

auto bond0
iface bond0 inet manual
		bond-slaves eno1 eno2
		bond-miimon 100
		bond-mode 802.3ad
		bond-xmit-hash-policy layer3+4

auto vmbr1
iface vmbr1 inet manual
        bridge-ports bond0
        bridge-stp off
        bridge-fd 0
        bridge-vlan-aware yes
        bridge-vids 2-4094
		
```

4. Apply changes
```bash
ifreload -a
```