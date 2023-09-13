# Cluster of two nodes breaks when one node shuts down
#Proxmox #Virtualization #Hypervisor #Clusters

These problem happens due to lack of Quorum. A Cluster needs to have at least two nodes, and each nodes has 1 quorum vote. So, if one of the nodes goes down, there are not enough quorum to maintain the cluster functional. One way to circumvent this problem, in case we wish to temporally shutdown one node in a cluster of two without breaking it is to give more quorum votes to the node that will remain on.

We can do that by editing the `/etc/pve/corosync.conf` file; But before you do it, make sure you create a backup copy of the file:

```bash
cp /etc/pve/corosync.conf /etc/pve/corosync.conf.bak
```

Next, open the file:
```
nano /etc/pve/corosync.conf
```

You should get something similar to this
```
logging {
  debug: off
  to_syslog: yes
}

nodelist {
  node {
    name: pve1
    nodeid: 1
    quorum_votes: 1
    ring0_addr: 172.16.11.10
  }
  node {
    name: pve2
    nodeid: 2
    quorum_votes: 1
    ring0_addr: 172.16.11.11
  }
}

quorum {
  provider: corosync_votequorum
}

totem {
  cluster_name: CAR-Cluster
  config_version: 1
  interface {
    linknumber: 0
  }
  ip_version: ipv4-6
  link_mode: passive
  secauth: on
  version: 1
}
```


Now, Lets say I am planning on shutting down pve2 temporally. Then all I need to do is to increase the `quorum_vote` of pve1 by one, that way the cluster will still have the minimum quorum required, even with the absence of pve2.

Edit the file and save it
```
  node {
    name: pve1
    nodeid: 1
    quorum_votes: 2
    ring0_addr: 172.16.11.10
  }
```
