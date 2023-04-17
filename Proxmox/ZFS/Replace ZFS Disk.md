[Source](https://forum.proxmox.com/threads/zfs-mirrored-rpool-disk-id-changed-cannot-zpool-replace.69915/)

1. The following command will print the current status of the ZFS pool and will also list the disks that makup the pools and other disks in the system.
```bash
zpool status -x
```

2. Grab the ID of the new device
in this example:
`ata-WDC_ZD10BADS-00M5B1_WD-WCAU4X307848`

3. Then run: 
```
zpool replace <poolname> <old ID> <new ID>
```
E.g.
```
zpool replace pool1 150421355511809598179 ata-WDC_ZD10BADS-00M5B1_WD-WCAU4X307848
```

