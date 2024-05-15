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

### Check if a particular user exists
```bash
passwd <username>
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

## Listing Hardware
### CPU Information
```bash
lscpu
```

###  Hardware
```bash
lshw
```

In case the command is not available. For Debian based distros:
```bash
sudo apt install lshw
```

You may want to run this command with `sudo` in order to see all the information.
```bash
sudo lshw
```

with the `-html` option this command will give you the output in html format. You can then save that into a file you can then open in a web browser.
```bash
sudo lshw -html > hwinfo.html 
```

A shorter output version of the same command.
```bash
sudo lshw -short
```

### USB devices
```bash
lsusb
```

Here we use the watch command, which will basically run the `lsusb` every two seconds. The `-d` option is for highlighting the differences in the output, which is particularly useful if you are trying to identify a device as you are plugging it in and out.
```bash
watch -d lsusb
```

Tree view
```bash
lsusb -t
```
### Storage
```bash
lsblk
```

You can run this command with `watch` in order to easily identify a usb external storage device
```bash
watch lsblk
```

### PCI bus
```bash
lspci
```



