# Advanced commands
#Linux 


## Monitor Disk Space on the terminal
```bash
watch df -h
```

## Discover other hosts in the same network
```bash
netdiscover -v <IP_address_of_router_in_CIDR_format>
```
It shows all IP addresses of devices connected to the same network

E.g. 
```bash
netdiscover -v 192.168.64.1/24
```

## Netstat command
This command lists all open ports in a server
```bash
netstat -tupln
```
`flags:   t=show tcp connections | u=show udp connections  | p= program that is attached to | l=show listening ports only | n=show addresses in numeric form``

It is best to run this command with root permissions: 
```bash
sudo netstat -tupln
```


## Bad command
This command is very destructive. Do not run on your system. Only for educational purposes. Run in a disposable VM only.

```bash
cat /dev/zero > /var/log/application.log
```

This command will fill up your file system in a heart beat, preventing you from even running commands, making it really hard to recover.

## Erase the contents of a file
This command will delete all the contents of a file. 
```bash
truncate -s 0 /var/log/application.log
```

This is an option for recovering a server with its file system full (Analog to the situation explained in the command above). The only downside is that you would lose information that could be useful for determining the cause of the problem.


## Hashing utility

```
echo -n "hello" | md5sum
```