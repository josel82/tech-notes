# Logical Volume Manager
#Linux #LVM #Storage 

Logical Volume Manager (LVM) is a software component that allows for the creation of logical volumes (LVs) on top of physical storage devices such as hard drives or solid-state drives. LVM provides a layer of abstraction between the operating system and the physical storage devices, allowing for more flexibility and dynamic allocation of storage resources.

With LVM, multiple physical storage devices can be combined into a single logical volume, which can then be partitioned into smaller logical volumes called logical partitions or logical volumes (LVs). These LVs can be resized, moved, or even moved to another physical storage device while the system is still running, without affecting the data stored on them.

LVM is commonly used in Linux operating systems but is also available on other platforms. It offers many benefits such as ease of management, improved performance, and enhanced reliability by providing a flexible and resilient storage infrastructure for both physical and virtual environments.
```xml
<img style="float: right;" src="">
```

![LVM Diagram](https://cdn.thegeekdiary.com/wp-content/uploads/2014/10/LVM-basic-structure.png)

## LVM Display commands

### Physical Volume info
```bash
sudo pvdisplay
```

### Volume Group info
```bash
sudo vgdisplay
```

### Logical Voume info
```bash
sudo lvdisplay
```

```bash
sudo lvs
```

## LVM commands

### Turning a HD into a Physical Volume
```bash
sudo pvcreate /dev/<device name>
```

### Adding Physical Volume to a Volume Group
```bash
sudo vgextend <vg-name> /dev/<devide name>
```

### Extending a Logical Volume
In the following example we are just extending the logical volume by 10GB. You can find the LV path with the `df -h` command.
```bash
sudo lvextend -L +10G /dev/mapper/lv--ubuntu-lv--root
```

### Resizing the File System
Once we have extended the Logical Volume, the next step is to rezise the file system, only then we will have this extra space available to use.
```bash
sudo resize2fs /dev/mapper/lv--ubuntu-lv--root
```

### Extending LV (100% Physical Volume)
Here we are extending the LV to take all the available space in the Physical Volume. Also notice the `--resizefs` option, this will resize the file system automatically when the command is run.
```bash
sudo lvextend --resizefs -l +100%free /dev/mapper/lv--ubuntu-lv--root
```

### Adding a new Volume Group and Logical Volume on a new HD
1. Create a Physical Volume.
```bash
sudo pvcreate /dev/sdb
```

2. Create a Volume Group.
```bash
sudo vgcreate vg-extra /dev/sdb
```

3. Create a Logical Volume.
```bash
sudo lvcreate vg-extra -L 5G -n lv-logs
```

4. Format the newly create LV.
```bash
sudo mkfs.ext4 /dev/vg-extra/lv-logs
```

5. Mount the new LV.
```bash
sudo mkdir -p /mnt/extra/logs
sudo mount /dev/vg-extra/lv-logs /mnt/extra/logs
```

6. Set up the system to automatically mount this LV when booting.
```bash
sudo blkid /dev/mapper/vg--extra-lv--logs
```
grab the UUID of the LV. Next create a backup copy of the `fstab` file:
```bash
sudo cp /etc/fstab /etc/fstab.bkp
```
Unmount the LV:
```bash
sudo umnount /mnt/extra/logs
```
Edit the `fstab` file:
```bash
sudo nano fstab
```
Add the following line to the file:
```
UUID=da97eef1-c433-4aca-a765-24af1f05fbce /mnt/extra/logs ext4 defaults 0 2 
```
Test the `fstab` file:
```bash
mount -a
```

## Snapshots
Create a snapshot. In this example we are creting a snapshot of a logical volume "lv-example".
```bash
lvcreate /dev/mapper/vg--extra-lv--example -L 1G -s -n example_snapshot_20230405 
```

Recover a file from a snapshot.
First unmout the LV you want to recover the file from.
```bash
sudo umount /mnt/extra/example
```
Restore the snapshot.
```bash
sudo lconvert --merge /dev/mapper/vg--extra-example_snapshot_20230405
```
Flush the original LV.
```bash
sudo lvchange -an /dev/mapper/vg--extra-lv--example
sudo lvchange -ay /dev/mapper/vg--extra-lv--example
```
Remount the LV.
```bash
sudo mount -a
```

## General Linux commands for displaying storage info

```bash
df -h
```

```bash
lsblk
```

```
cat /etc/fstab
```