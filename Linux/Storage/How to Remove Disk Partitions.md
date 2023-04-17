# How to Remove Disk Partitions
#Linux #Storage 

1. Run the fdisk utitly on the target disk
```bash
fdisk /dev/sda
```

2. Press "p" to see partition information
```
Welcome to fdisk (util-linux 2.33.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Command (m for help): p
```

3. Then press "d" to delete partition. In this example we have two partitions: 
`/dev/sda1`
`/dev/sda9`
select one of them and press enter.
```
Command (m for help): d
Partition number (1,9, default 9): 9
```

4. Delete the remaining partition
```
Command (m for help): d
Selected partition 1
Partition 1 has been deleted.
```

5. Check that the partitions have been deleted
```
Command (m for help): p
```

6. Once you have confirmed that the partitions have been deleted, you can proceed to write the changes to the disk.
```
Command (m for help): w
```
