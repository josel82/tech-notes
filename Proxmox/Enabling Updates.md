# Enabling Updates
#Proxmox #Linux #Virtualization #Hypervisor 

## Unstable updates
1. Edit `sources.list` file.
```bash
nano /etc/apt/sources.list
```
add a line for the non-production updates for proxmox. Save the file and exit.
```
# not for production use
deb http://download.proxmox.com/debian buster pve-no-subscription
```

2. Edit the `pve-enterprice.list` file. 
```bash
nano /etc/apt/sources.list.d/pve-enterprise.list
```
Comment this line out, save the file and exit.
```
# deb http://enterprise.proxmox.com/debian/pve buster pve-enterprise
```

3. Update the lists.
```bash
apt-get update
```

4. Do a distribution upgrade.
```bash
apt-get dist-upgrade
```

5. Reboot your server.
```
reboot now
```
