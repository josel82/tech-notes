# Enabling the No Subscription Repository
#Proxmox 

## GUI method (recommended)
1. Select the target node.
2. Go to "Repositories"; On the main menu, under Updates > Repositories.
	1. Disable the Enterprise repository. This is located in `/etc/apt/sources.list.d/pve-enterprise.list`. Select the Repository, then click on disable.
	2. Add the No subscription Repository. Click on Add, a "No valid subscription" warning will popup just click on OK. In the next popup window, on the "Repository" dropdown menu select No subscription and accept.

## Manual method
1. We can disable the Enterprise repository by editing the following file:
```bash
nano /etc/apt/sources.list.d/pve-enterprise.list
```

We just need to comment out this line.
```
# deb https://enterprise.proxmox.com/debian/pve bookworm pve-enterprise
```

2. Add the No Subscription repository:
```bash
nano /etc/apt/sources.list
```

The last line enables the No Subscription repository. As of now, this is the latest version of Proxmox 8. At the moment you are reading this, you may want to add a most resent version.
```
deb http://ftp.ie.debian.org/debian bookworm main contrib

deb http://ftp.ie.debian.org/debian bookworm-updates main contrib

# security updates
deb http://security.debian.org bookworm-security main contrib


# not for production use
deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription
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