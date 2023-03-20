# How to stop stuck VMs
#Proxmox #Hypervisor #Virtualization #VMs

1. Log in to proxmox node shell.
2. List the current locks and dentify the one is giving you problems.
```bash
ls -l /run/lock/qemu-server
```

3. Delete the lock.
```bash
rm -f /run/lock/qemu-server/lock-<VM ID>.conf
```

4. Verify you have deleted the correct lock.
```bash
ls -l /run/lock/qemu-server
```

5. Stop the virtual machine.
```bash
qm stop <VM ID>
```
