# K3S

## Installing K3S on Debian distros
Disable UFW on the host
```jsx
ufw disable
```

## Minimum requirements

|Node|CPU|RAM|
|---|---|---|
|Server|2 cores|2GB|
|Agent|1 core|512MB|

### Disk
It is recommended using an SSD for the datastore when possible. If deploying K3s on a Raspberry Pi or other ARM devices, it is recommended that you use an external SSD. etcd is write intensive; SD cards and eMMC cannot handle the IO load.

### Networking
The K3s server needs port 6443 to be accessible by all nodes.

## Config file
```bash
/etc/rancher/k3s/k3s.yaml
```

## HA Deployment
### Topology

|**Node**|**IP address**|
|---|---|
|loadbalancer|10.1.20.50|
|master1|10.1.20.51|
|master2|10.1.20.52|
|master3|10.1.20.53|
|worker1|10.1.20.54|
|worker2|10.1.20.55|

- On **master1**
```bash
curl -sfL <https://get.k3s.io> | K3S_TOKEN=token sh -s - server \\
  --cluster-init \\
  --tls-san 10.1.20.50 \\
  --node-taint CriticalAddonsOnly=true:NoExecute
```

- On **master2** and **master3**
```bash
curl -sfL <https://get.k3s.io> | K3S_TOKEN=token sh -s - server \\
  --server <https://10.1.20.50:6443> \\
  --tls-san 10.1.20.50 \\
  --node-taint CriticalAddonsOnly=true:NoExecute
```

- On worker1 and worker2
```bash
curl -sfL <https://get.k3s.io> | K3S_TOKEN=JVJi7_C_UKzF sh -s - agent --server <https://10.1.20.50:6443>
```

- On the development computer
    
    MacOS
```bash
brew install kubectl
```

copy the configuration from one of the master nodes
```bash
/etc/rancher/k3s/k3s.yaml
```

and paste it into
```bash
~/.kube/config
```

in your development computer

## Uninstalling K3S

On the masters
```bash
/usr/local/bin/k3s-uninstall.sh
```

On the agents
```bash
/usr/local/bin/k3s-agent-uninstall.sh
```

Removing a node from the cluster
```bash
kubectl delete node master3
```

Troubleshooting
```bash
journalctl -xeu k3s.service
```

```bash
systemctl status k3s.service
```