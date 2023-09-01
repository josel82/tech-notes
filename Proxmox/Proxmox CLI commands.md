# Proxmox CLI commands
#Proxmox #Hypervisor #Virtualization #VMs #LXC 

## Virtual Machines

- List Virtul Machines
```bash
qm list
```

- Start a VM
```bash
qm start <VM ID>
```

- Shootdown
```bash
qm reboot <VM ID>
```

- Reboot a VM
```bash
qm reboot <VM ID>
```

- Reset a VM (hard reboot)
```bash
qm reset <VM ID>
```

- Stop a VM (hard shootdown)
```bash
qm stop <VM ID>
```

- Unlock VM
```bash
qm unlock <VM ID>
```

- List information about a VM
```bash
qm config <VM ID>
```

- Configuring VM Options
```bash
qm set <option> <VM ID>
```
e.g:
```bash
qm set --onboot 0 100
```
connect to a VMs console
```bash
qm terminal <VM ID>
```

## Containers

- List Containers
```bash
pct list
```

- Get info about a container
```bash
pct config <VM ID>
```

- Start a container
```bash
pct start <VM ID>
```

- Shutdown container
```bash
pct shutdown <VM ID>
```

- Reboot container
```bash
pct reboot <VM ID>
```

- Stop a containerv (hard shutdown)
```bash
pct stop <VM ID>
```

- Access container
```bash
pct enter <VM ID>
```

- Change container options
```bash
pct set <VM ID> <option>
```
e.g:
```bash
pct set 200 -onboot 1
```

