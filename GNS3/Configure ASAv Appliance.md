# Configure ASAv Appliance
#GNS3 #Networking 

[Documentation](https://bluenetsec.com/asa-gets-stuck-on-boot-in-eve-ng/)

This fixes the issue of the appliance not booting up.

1. Start the appliance
2. Open VNC Viewer an connect to the appliance using the respectivew IP address and port number (Console is set to VNC by default | No password required)
3. Run the following commands:

```cisco
ciscoasa>enable
ciscoasa#conf t
ciscoasa(config)#cd coredumpinfo
ciscoasa(config)#copy coredump.cfg disk0:/use_ttyS0
```

4. Close the connection
5. Stop the appliance and change the console to "Telnet"

