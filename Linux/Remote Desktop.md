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