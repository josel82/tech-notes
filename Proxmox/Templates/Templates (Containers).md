# Templates (Containers)
#Proxmox #Virtualization #Hypervisor #Containers #LXC #Linux

## Preparation

1. Create and start the container you want to convert into a template. Access the shell of the container.

2. Create a user 
By default SSH as root is denied, for this reason we need to create a user to be able to ssh to this container.
```bash
adduser jamesh
```

2. Add user to the `sudo` group
```bash
usermod -aG sudo jamesh
```

3. Update Packages 
```bash
apt update && apt dist-upgrade -y
```

```bash
apt clean
```

```bash
apt autoremove
```


4. Delete SSH Host Keys
```bash
rm /etc/ssh/ssh_host_*
```
At this point you don't want to disconnect from the session, because you wouldn't be able to access the container without these host keys

5. Wipe the "machine-id" file
```bash
truncate -s 0 /etc/machine-id
```

6. Power off the container
```bash
sudo poweroff
```


## Convert container into a template

Once the Template has been created you can now clone this container.

## Configure Clones
login into the container. Delete the SSH Host keys once again. Regenerate the keys
```bash
sudo rm /etc/ssh/shh_host_*
```

```bash
sudo dpkg-reconfigure openssh-server
```
