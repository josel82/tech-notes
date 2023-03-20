# Formating and Mounting Storage Volumes
#Linux #Storage 

## List attached block devices
```bash
lsblk
```

another way of listing storage devices:
```bash
sudo fdisk -l
```

## List mounted devices
```bash
mount
```

You can be more specific using the pipe command:
```bash
mount | grep sdb
```


## How to unmount a Storage Device
First identify the device by running the `lsblk` command. In the case of USB Sticks try  connecting the device and running `lsblk` again. That way it will be obvious what device from all in the list is the one that you are targeting.

Once you have identify the device. run:
```bash
sudo umount /dev/device_name
``` 
E.g.:
```bash
sudo umount /dev/sdb1
```
or
```bash
sudo umount /mount/point
```
E.g.:
```bash
sudo umount /media/myUser/disk
```

## How to erase a Storage Device
Once the device has been unmounted, we can erase it by creating a new partition table on it.
```bash
sudo fdisk /dev/device_name
```

The `fdisk` command will prompt you for a command. You can list the different commands available by typing 'm' and pressing enter. Here is a list of them:
```bash
<<
Command (m for help): m
  
Help:
  
  GPT
   M   enter protective/hybrid MBR
  
  Generic
   d   delete a partition
   F   list free unpartitioned space
   l   list known partition types
   n   add a new partition
   p   print the partition table
   t   change a partition type
   v   verify the partition table
   i   print information about a partition
  
  Misc
   m   print this menu
   x   extra functionality (experts only)
  
  Script
   I   load disk layout from sfdisk script file
   O   dump disk layout to sfdisk script file
  
  Save & Exit**
   w   write table to disk and exit
   q   quit without saving changes
  
  Create a new label
   g   create a new empty GPT partition table
   G   create a new empty SGI (IRIX) partition table
   o   create a new empty DOS partition table
   s   create a new empty Sun partition table
```

In this example we are going to create a GPT partition table. all we need to do is to type 'g' and press enter:

```bash
<<
Command (m for help): g
  
Created a new GPT disklabel (GUID: FA89E289-ADDD-5940-BDE9-BD7D4F27CC4E).
The device contains 'iso9660' signature and it will be removed by a write command. See fdisk(8) man page and --wipe option for more details.
```

You can list the partitions in your storage device by entering the 'p' option. You should have no partitions listed since you have just created a new partition table.

## Create a new partition

You can create a new partition by entering the 'n' option. 

```bash
<<
Command (m for help): n
Partition number (1-128, default 1): 
First sector (2048-62333918, default 2048): 
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-62333918, default 62333918): +1.2G
  
Created a new partition 1 of type 'Linux filesystem' and of size 1.2 GiB.
```

Here I selected the default value for the first sector but gave it a different value for the last sector because I didn't want to assign all the space to this partition. I did this by entering '+1.2G' which will make this partition 1.2GB 

Then I created a secon partition by entering the 'n' option once again:

```bash
<<
Command (m for help): n
Partition number (2-128, default 2): 
First sector (2519040-62333918, default 2519040): 
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2519040-62333918, default 62333918): 
  
Created a new partition 2 of type 'Linux filesystem' and of size 28.5 GiB.
```

In this ocation I selected the default values for the First and Second sectors because I just wanted to create a second partition that would take the rest of the space available.

Finally, enter the option 'w' to make the changes final.

## Format the newly created partitions

Now that we have partitioned our drive, we are ready to format it. Now, here we need to stop for a moment to decide which type of file system we want to give this device. This will depend of the of the type of device (internal drive or external drive) and which operating system I intend to use the drive for (Linux, MacOS or Windows). 

Asuming we wanted to use this device as an external drive for a Linux machine, we wil proceed as follows:

```bash
sudo mkfs.ext4 /dev/device_partition
```
E.g.:
```bash
sudo mkfs.ext4 -L label /dev/sdb1
```

	The 'L' option is for adding a label to the device.

In cases where I plan to use the device in multiple operating systems I would have to run:
``
```bash
sudo mkfs.exfat -n "label" /dev/sdb1
```

However, to be able to run this command you'll need to install the following packages first:

```bash
sudo apt install exfat-utils exfat-fuse
```


## How to mount a drive
In Linux mounting a drive is the act of attaching the storage volume to a directory in the host file system.

The most apropriate directories for attaching storage volumes are the 'mnt' and 'media' directories.

The 'media' directory is used for attaching temporary storage volumes. External HD, USB Keys, etc; While the 'mnt' directory is used for attaching permanent volumes.

You will mount the drive with the following command:
`sudo mount /dev/<device partition> /media/<directory>`  (create a new directory if it doesn't exist) 
E.g.:
```bash
sudo mount /dev/sdc1 /media/external/
```

You can verify that the drive is mounted with:
```bash
lsblk
``` 
and 
```bash
df -h
```

## NCDU
This is a very useful tool used for scanning your file system and see which folders take the most amount of space.

Often this tool doesn't come install by default, in those cases you will need to install it on your system:
```bash
sudo apt install ncdu
```

and you use it as follows:

```bash
sudo ncdu /path
```

E.g.: 
```bash
sudo ncdu /
```  
here ncdu will scan all your file system

Note: you want to run this comman with sudo, otherwise it will not show those folders your user don't have permission to see.

You can run this command with the 'x' option if you want to only scan the local volumes and exclude all mounted devices:

```bash
sudo mcdu / -x
```
