# Transferring files into Proxmox server
#Proxmox #Hypervisor 

Open up your terminal and navigate to the directory containing the files you want to copy into your server.

In this example I am importing all files (\*) in the current local directory into the specified path in the Proxmox server on which we are connecting as root using a local domain name. 
```bash
scp * root@proxmox.mylab.home:/var/lib/vz/template/qemu
```

