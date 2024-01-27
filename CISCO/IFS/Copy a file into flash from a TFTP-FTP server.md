# Copy a file into flash from a TFTP-TFP server
#CISCO #IOS 


## Copy form TFTP server

1. Make sure you device is able to communicate with the TFTP server. 
2. From the Cisco device in EXEC mode, run:
```
copy tftp flash
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
dir flash0:
```

4. You can also use the following command:
```
show flash
```


## Copy form FTP server
Quite similar to the previous commands you can run the following command in EXEC mode:
```
copy ftp flash
```
and  follow the prompts.

You can also be more specific by running the following command:
```
copy ftp://admin:cisco@192.168.1.100/c2900-universalk9-mz.SPA.150-1.M2.bin flash
```
where
- username: admin
- password: cisco
- FTP server IPv4 address: 192.168.1.100
- Filename: c2900-universalk9-mz.SPA.150-1.M2.bin
- Destination: flash0:

## Configure Username and Password in the router

```
ip ftp username admin
ip ftp password cisco
```

Doing this simplifies the previous command. Once you have configure an FTP Username and Password, you can run the copy command as follows: 

```
copy ftp://192.168.1.100/c2900-universalk9-mz.SPA.150-1.M2.bin flash
```