# Import Virtual Disks into a VM
#Proxmox #Virtualization  #VMs

[Documentation](https://ostechnix.com/import-qcow2-into-proxmox/)

For purpose of this documentation we will assume we have two disks `vm-disk-0.qcow2` and `vm-disk-1.qcow2` stored in `/home/myUser/images`  and we want to import these two disks into a new VM

Create a new VM with ID: 110 (This ID is just a aleatory number used for this example, you could select any other available number). On the "OS" section select "Do not use any media" option. You can continue with the default options.

## Proceadure 1

^919a14

Once the VM has been created, you can delete the virtual disk that was created by default.

Log into the node's shell; Then run the following commands to import the two disks:
```bash
qm importdisk 110 /home/myUser/images/vm-disk-0.qcow2 VM-Drives --format qcow2
```

```bash
qm importdisk 110 /home/myUser/images/vm-disk-1.qcow2 VM-Drives --format qcow2
```

In this example "VM-Drives" is the name of the directory for Disk Images 

These two disks will show in VM 110 as unused disks. You will then need to attach them to the VM.

Once this has been done, on the VM menu got to Options > Boot Order and change it to boot from the appropiate disk.

## Proceadure 2
After the VM has been created, add another virtual disk with the default values. Then, detach both disks. 

Log into the node's shell. List the names of these newly created disks.
```
ls -l /pool_name/vm-drives/images/110/
```

```
-rw-r----- 1 root root 524368281600 Mar 30 17:26 vm-110-disk-0.qcow2
-rw-r----- 1 root root  20974993408 Mar 30 17:26 vm-110-disk-1.qcow2
```

Now we are going to replace this files with the once we want to import
```bash
mv /home/myUser/images/vm-disk-0.qcow2 /pool_name/vm-drives/images/110/vm-110-disk-0.qcow2
```

```bash
mv /home/myUser/images/vm-disk-1.qcow2 /pool_name/vm-drives/images/110/vm-110-disk-1.qcow2
```

Back in the Web UI. Select VM 110. The click on "Hardware", add the disks back by selecting them, then pressing "Edit" and finally clicking on  "Add".

Ammend the Boot Order.

Start the VM

## Procedure 3
Import a disk image from the internet
1. Copy the link of the image download
2. Log into the node's shell and run the following command:
```bash
wget https://image.download.url
```

3. Chances are that the downloaded file is compressed. `disk_image.qcow2.xz`
4. Decompress the file as follows:
```bash
xz -d -v disk_image.qcow2.xz
```

5. [[Import Virtual Disks into a VM#^919a14]]
