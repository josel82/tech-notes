# Enable built-in TFTP server
#MacOS #IT 



1. Enable the TFTP server by running:
```
sudo launchctl load -F /System/Library/LaunchDaemons/tftp.plist
```
You will be prompted for user authentication.

2. Next run:
```
sudo launchctl start com.apple.tftpd
```

You can confirm that the server is running with the following command:
```
netstat -atp UDP | grep tftp
 udp4     0    0  *.tftp                *.*
 udp6     0    0  *.tftp                *.*
```

The TFTP server should be now running on port 69 waiting for connections. 

3. You should place the files you want to serve into the `/private/tftpboot` directory.
4. Change the permissions of the directory above:
```
sudo chmod 777 /private/tftpboot
sudo chmod 777 /private/tftpboot/*
```

5. To shutdown the server, run the following command:
```
sudo launchctl unload -F /System/Library/LaunchDaemons/tftp.plist
```

6. Check that the server is not longer running:
```
netstat -atp UDP | grep tftp
```
You should get no output this time