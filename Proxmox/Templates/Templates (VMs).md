# Templates (VMs)
#Proxmox #Virtualization #Linux 

Source:
[Proxmox VE - How to build an Ubuntu 22.04 Template (Updated Method)](https://www.youtube.com/watch?v=MJgIm03Jxdo&t=922s)

## Create a new virtual machine 

1. Give the VM a name and an ID
![create-vm-01.png](Images/create-vm-01.png)

2. Next, select 'Do not use any media' 
![create-vm-02.png](Images/create-vm-02.png)

3. Leave everything with its deafaul values, but make sure you tick the 'Qemu Agent' option.
![create-vm-03.png](Images/create-vm-03.png)

4. Under 'Disks', delete the default disk. We will be importing a disk image.
![create-vm-04.png](Images/create-vm-04.png)

5. Keep the default value of 1 core. You will be able to add more cores to each individual clone if required.
![create-vm-05.png](Images/create-vm-05.png)

6. Give this template 1024MB of RAM. You can increase the memory on each individual clone if required.
![create-vm-06.png](Images/create-vm-06.png)

7. Select the right Bridge and VLAN tag  
![create-vm-01.png](Images/create-vm-12.png)

8. Check that all the setting are correct and click on 'Finish'.
![create-vm-02.png](Images/create-vm-08.png)

## Add a Cloud-Init drive
1. Select the newly created VM. On the Menu, select 'Hardware', then click on 'Add', then select 'CloudInit Drive'.
![cloud-init-01.png](Images/cloud-init-01.png)

2. Select the Storage Pool that corresponds to your system.
![cloud-init-02.png](Images/cloud-init-02.png)

## Set up Cloud-Init user and password.
Here you can add a SSH Public Key if you have generated one. You can also set the VM to obtain an IP address via DHCP under the 'IP Config' option.
![cloud-init-03.png](Images/cloud-init-03.png)

## Import Cloud-Init image
In this example, I am going to be using Ubuntu 20.04 focal as the OS version of my Cloud-Init image.

1. Open this [link](https://cloud-images.ubuntu.com/minimal/releases/focal/release) on a web browser and copy the link of the image. Copy the Link address of the cloud-init image. It is the file with the `.img` file extension.

![cloud-init-04](Images/cloud-init-04.png)

2. Log in to your Proxmox node terminal and download the images as follows:
```bash
wget https://cloud-images.ubuntu.com/minimal/releases/focal/release-20200423/ubuntu-20.04-minimal-cloudimg-amd64.img
```


3. Chance the name of the image, making sure that you set the file extension to `.qcow2`
```bash
mv ubuntu-20.04-minimal-cloudimg-amd64.img ubuntu-20.04.qcow2
```

4. Resize the image.
```bash
qemu-img resize ubuntu-20.04.qcow2 32G
```

5. Import disk into the VM.
```bash
qm importdisk 900 ubuntu-20.04.qcow2 <local-storage>
```

6. Create a VGA console for the VM .
```bash
qm set 900 --serial0 socket --vga serial0
```

7. Attach the disk image into the VM. 
On the Web UI, select the VM and under 'Hardware' you will see an 'Unused' virtual disk. Select the disk, then click on 'Edit', finally click on 'Add'.

8. Edit the boot order.
Under 'Options', select 'Boot Order' and click on 'Edit'.
![boot-order-01.png](Images/boot-order-01.png)

Drag the 'scsi0' disk to the second position and click OK
![boot-order-02.png](Images/boot-order-02.png)


## Convert the VM into a Template
Right click on the VM, then click on 'Convert to template'.
![template-01.png](Images/template-01.png) ^273ddd


## Crate a Full Clone of the template
1. Right click on the template. Select 'Clone'.
![clone-vm-01.png](Images/clone-vm-01.png)

2. Give the clone a name and ID. Set the Mode as 'Full Clone'. Select your Target Storage, then click on 'Clone'.
![clone-vm-02.png](Images/clone-vm-02.png)

3. Start the Clone

## Install qemu agent on the clone
1. Once started, log in to the clone's terminal and run the following command:
```bash
sudo apt install qemu-guest-agent
```

2. Reboot the VM

