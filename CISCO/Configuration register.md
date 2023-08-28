In cisco devices this is a 4 digit hexadecimal number that is used to change the behaviour of the router.
the default value of the configuration register is:
#### 0x2102
The last number determines how the router boots
In Cisco, the 0x indicates that the following numbers are hexadecimal. The same number would have the following value in binary:
#### 0010 0001 000 0010

Here is the list of things you can configure with the configuration register:
-   How the router boots (into ROMmon, NetBoot)   
-   Boot Options (ignore configuration, disable boot messages)
-   Console speed (baud rate for a terminal emulation session)

You can change the configuration register as follows:
`Router(config)#configuration-reggister 0x2100`
This will configure this router to boot in ROMMON mode. You will be asked to reboot the device for this change to take effect

#### For CCNA

0x2102  Default configuration
0x2100 Boot in ROMMON mode
0x2142 Bypass startup configuration
0x2101 Boot in RxBoot if supported (newer routers will boot with the first operating system in flash)

#### Booting configuration

`Router(config)#boot system flash <IOS file>`

other options
- ftp
- mop
- rcp
- rom
- tftp
