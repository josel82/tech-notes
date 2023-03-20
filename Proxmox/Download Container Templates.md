# Download Container Templates
#Proxmox #Virtualization #Hypervisor #LXC #Containers #Templates

1. From the shell of your Proxmox node, update container template database:
```bash
pveam update
```

2. List available templates.
```
pveam available
```

3. Once you have found the template you want to download, go ahead and copy the file name and paste it to the following command
```bash
pveam download <pool_name> <template_file>
```
