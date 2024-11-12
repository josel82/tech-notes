# Removing a node from a cluster
#Proxmox #Virtualization 

1. Switch shutdown the node you intend to remove from the cluster, making sure you never connect it again to the same network. (Reconnecting a removed node to the same network causes issues). In the case you wanted to rejoin this node, you will need to re-install proxmox on the node from scratch.
2. Only after the node is shutdown. Open a terminal on the master node. Run the following command as root: 
```bash
pvecm delnode <nodename>
```
3. After removing the node you may still see the node on the GUI. To remove the node from the GUI you need to delete the following directory:
```bash
rm -r /etc/pve/nodes/<nodename>
```
4. Reload the GUI and the node should be gone.

## Remove cluster
```
pvecm expected 1
systemctl stop pve-cluster 
pmxcfs -l
rm -f /etc/pve/cluster.conf /etc/pve/corosync.conf
rm -f /etc/cluster/cluster.conf /etc/corosync/corosync.conf
rm /var/lib/pve-cluster/.pmxcfs.lockfile
systemctl stop pve-cluster 
```

reboot the system


### Revert ProxMox from orphaned cluster node, back to standalone server.

[Raw](https://gist.github.com/RobSeder/ec95bf6600b1546186d6f8c7f0706c97/raw/1f5053dc7b80ec05427d2d2135f2897a4a8ee0a9/revert.sh)