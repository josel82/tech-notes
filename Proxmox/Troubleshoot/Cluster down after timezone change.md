# Cluster down after timezone change


Problem:

Nodes were down causing the cluster to crash due to lack of quorum.

Nodes were throwing the following errors
```
Failed to reload daemon: Transport endpoint is not connected
Failed to retrieve unit state: Transport endpoint is not connected
Failed to get unit file state for pve-ha-crm.service: Transport endpoint is not connected
```


Found the solution in the linked post

[Source](https://forum.proxmox.com/threads/broken-system-files-after-reboot.109327/)

1. Boot in recovery mode
2. Change tome zone
```
ln -sf /usr/share/zoneinfo/Etc /etc/localtime
```