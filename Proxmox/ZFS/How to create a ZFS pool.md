# How to create a ZFS pool

[Video](https://www.youtube.com/watch?v=oSD-VoloQag&t=915s)

1. Select the pve node.
2. Under "Disks", select ZFS, then click on "Create ZFS"
3. A windows pops up. Give this pool a name, select the type of RAID and untick the "Add Storage" option. You may need to format the disks you want to use in this pool, in case they don't appear in the lists of unused disks. [[How to Remove Disk Partitions]]. Select "lz4" as Compression type, Finally, select the disks and click on "Create"
4. Run smartctl on your disks
```bash
smartctl -a /dev/sda
```

5. Create datasets. Lets start by listing the existing datasets 
```bash
zfs list
```
```
NAME      USED  AVAIL      REFER   MOUNTPOINT
myPool    396   1.76T       96K    /myPool
```
Then you can run:
```bash
zfs create myPool/backups
```

```bash
zfs create myPool/isos
```

```bash
zfs create myPool/vm-drives
```

6. Back in the Web UI, click on "Datacenter", then click on "Storage" and select "Directory", then click on the "Add" button. Give this directory a name under "ID". Paste the path to the dataset under "Directory". Select the types of data you want to store here, e.g. Disk Image, Backup, etc. Leave the rest as default. Click on Add.