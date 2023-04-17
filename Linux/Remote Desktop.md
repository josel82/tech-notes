# Remote Desktop
#Linux #VNC #Windows

## Prerequisite
- VNC client software.
- The server you intend to connect to must be reachable over the internet.

If you are in a debian based distro that doesn't have a VNC viewer, you can install one with:
```bash
sudo apt install tigervnc-viewer
```

## How to connect to remote server via VNC

1. Build a tunnel
```bash
ssh -L 61000:localhost:5901 -N -f username@178.79.190.211
```

 2. Once you run this command you can now connect with your VNC viewer with the following URI: `localhost:61000`

3. Type **vncviewer** on your terminal. A popup will appear. Type in the same URI: `localhost:61000`

## Closing the tunnel

1. First get the process ID with:
```bash
ps aux | grep 5901
```

2. Kill the process
```bash
kill -9 <PID>
```


#### In Windows

1. Find the process ID
```msdos
netstat -ano | find <ip_address>
```

2. Kill the process
```msdos
Taskill /F /PID <PID>
```


## TightVNC 

[Source](https://www.youtube.com/watch?v=3K1hUwxxYek&t=77s)

```bash
sudo apt update 
```

```bash
sudo apt install lightdm 
```

```bash
sudo reboot 
```

```bash
sudo apt install x11vnc
```

Create the following config file:
```bash
sudo nano /lib/systemd/system/x11vnc.service
```

Paste the following lines inside of the file above:
```
[Unit] 
Description=x11vnc service 
After=display-manager.service network.target syslog.target 

[Service] 
Type=simple 
ExecStart=/usr/bin/x11vnc -forever -display :0 -auth guess -passwd password ExecStop=/usr/bin/killall x11vnc 
Restart=on-failure 

[Install] 
WantedBy=multi-user.target
```

Save the file and run the following commands:

```bash
sudo systemctl daemon-reload 
```

```bash
sudo systemctl enable x11vnc.service 
```

```bash
sudo systemctl start x11vnc.service 
```

```bash
sudo systemctl status x11vnc.service
```