# VNC Troubleshoot
#GNS3 #Issues #Troubleshoot

## Problem
I am not able to connect to appliance via VNC. I get the following error: 
```
Could not start VNC program with command 'vncviewer 10.1.20.15:5900': [Errno 2] No such file or directory: 'vncviewer'
```

## Cause
You host OS doesn't have a VNC client installed. That's the reason why GNS3 is complaining that it isn't able to find the `vncviewer` command.

## Solution
Install a VNC client on your host OS. This will vary depending on the Operating System, but it is important that the VNC client has the same start command (vncviewer), otherwise you will have to edit the `Console application command for VNC`, under **Preferences > General > VNC**
