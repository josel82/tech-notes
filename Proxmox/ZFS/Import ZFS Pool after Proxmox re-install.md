# Import ZFS Pool after Proxmox re-install
#Proxmox #Virtualization #ZFS

[Source](https://www.thomas-krenn.com/en/wiki/ZFS_Pool_Import_-_Proxmox_single_host_reinstall_without_full_backup)

Log in to your Node's shell and run the following commands:

List the existing ZFS pools
```bash
zpool list
```

List datasets
```bash
zfs list
```

Import a pool
```bash
zpool import -f pool_name
```

