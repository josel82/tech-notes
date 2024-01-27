# IOS File System (IFS)

#CISCO #IT 

For each physical memory device in the router, IOS creates a simple IOS file system and gives that device a name.

## List file systems
EXEC command:
```
show file system
```

After running the command above, you may notice around 20 different IOS file systems, but the router doesn't have 20 different physical storage devices. Instead, IOS uses these file systems for other purposes as well, with these types:
- **Opaque:** to represent logical internal file systems for the convenience of internal functions and commands
- **Network:** to represent external file systems found on different types of servers for the convenience of reference in different IOS commands
- **Disk:** for flash
- **Usbflash:** for USB flash
- **NVRAM:** a special type of NVRAM memory, the default location of the startup-config file


## A file's formal filename
The formal name of a file uses the prefix as seen in the far right column of the output of  the`show file system` command.
E.g.
```
more flash0:/wotemp/fred
```
This command would display contents of `fred` in directory `/wotemp` in the first flash memory slot in the router.

Many commands use a key-word that indirectly refers to a formal filename:

- `show running-config`: refers to `system:running-config`
- `show startup-config`: refers to `nvram:startup-config`
- `show flash`: refers to default flash IFS, usually `flash0`
