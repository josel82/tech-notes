# Copy a file into flash from a TFTP server
#CISCO #IT 

1. Make sure you device is able to communicate with the TFTP server. 
2. From the Cisco device, run:
```
Router#copy tftp: flash:
```

```
Address or name of remote host []? 192.168.1.67
Destination filename []? myfile.txt
Accessing tftp://192.168.1.67/myfile.txt !!!!!
Loading myfile.txt from 192.168.1.67 (via FastEthernet0/0): !
[OK - 120 bytes]

120 bytes copied in 0.623 secs (192 bytes/sec)
```

3. Check that the file has been copied:
```
Router#dir flash:
```
