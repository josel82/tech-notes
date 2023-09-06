# Basic commands
#Linux #Commands 

### Obtain OS version
```bash
lsb_release -a
```

### Print OS information
```bash
cat /etc/os-release
```

### List terminal sessions
```bash
w
```

### Check if a particular command exists in your system
```bash
command -v sshfs
```

### List processes
```bash
top
```
or
```bash
htop
```
`htop` has a nice interface, but it may require to be installed. 



### Man command
This command will open the man pages of any other command:
```bash
man cp
```
The example above will open the man pages for the `cp` command

### Process Status
```bash
ps aux
```
`flags: a=Display information about other users' processes as well as your own | u=Display the processes belonging to the specified usernames | x= When displaying processes matched by other options, include processes which do not have a controlling terminal`

### Lsof command
Lists all open files in a linux system
```bash
lsof
```
We can use the lost command to find the process using a specific port with the -i :port_number option.
```bash
lsof -i :[port]
```
`
### Stop a running process
```bash
Kill -9 <PID>
```


### Server shutdown
```bash
sudo shutdown
```
It shutsdown the server after one minute.

If you preffer an inmediate shutdown:
```bash
sudo shutdown now
```

### Server reboot
```
sudo reboot
```
It reboots the server after one minute.

Inmediate reboot
```bash
sudo reboot now
```

### Show routing table
```bash
route -n
```

### List CPU Information
```bash
lscpu
```

### List Hardware
```bash
lshw
```

### Hardware info
```bash
hwinfo
```

### List Hard Drives
```bash
lsblk
```
### List PCI
```bash
lspci
```

### List USB devices
```bash
lsusb
```



