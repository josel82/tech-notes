# Removing a node from a cluster
#Proxmox #Virtualization 

1. Switch shutdown the node you intend to remove from the cluster, making sure you never connect it again to the same network. (Reconnecting a removed node to the same network causes issues). In the case you wanted to rejoin this node, you will need to re-install proxmox on the node from scratch.
2. Only after the node is shutdown. Open a terminal on the master node. Run the following command as root: 
```bash
pvecm delnode <nodename>
```
3. After removing the node you may still see the node on the GUI. To remove the node from the GUI you need to delete the following directory:
```bash
rm -r /etc/pve/node/<nodename>
```
4. Reload the GUI and the node should be gone.