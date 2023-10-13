
```
show version
```


## File system

Lists the contents of the default file system:
```
show flash
```

```
show file systems
```
[[File system#^c0e03a]]


## Config files
Displays the running config found in `system:`
```
show running-config
```
Displays the startup config found in `nvram:`
```
show startup-config
```


## Control Plane
```
show control-plane host open-ports
```

## Filters
### Include
Only shows lines that contains the word after the include command
```
show run | include boot
```

### Begin
Outputs everything from the line that matches the word, whin in this examples happens to be "enable"
```
show run | begin enable
```

### Section
prints only the a section of the running config
```
show run | section line
```



## Lines

Lists active lines
```
show users
```

Closes a specified session
```
clear line <Line number>
```

lists all available lines on the device
Lists all active sessions
```
show sessions
```

disconnect the last active session
```
show sessions disconnect
```

takes you to a specified session e.g. `Router#1` will take you to session number 1
```
show sessions <session number>
```

## SSH
Lists status information for the SSH server, including the SSH version
```
show ip ssh
```
 
Lists status information for the current SSH connections into and out of the local switch
```
show ssh
```

Lists the public and shared key created for the use with SSH using the `crypto generate rsa` global configuration command
```
show crypto key myPubKey rsa
```
## Access Lists
```
show access-lists
```

```
show access-list <number>
```

## Switch

### Interfaces

```
show interfaces status
```

Lists a single line of output:
```
show interfaces f0/1 status
```

Detailed set of messages about the interface:
```
show interfaces f0/1
```

Displays the switchport information of a specific interface
```
show interfaces f0/1 switchport
```

Lists statistics about incoming and outgoing frames on the interfaces:
```
show interfaces f0/1 counters
```

Running config of a specific interface:
```
show run int g0/0
```

Lists trunk interfaces:
```
show interfaces trunk
```
### Mac address table

```
show mac address-table
```

Output all the dynamically learned MAC addresses only.
```
show mac address-table dynamic
```

Search for a specific mac address:
```
show mac address-table dynamic address 0200.1111.1111
```

Lists all mac address learned from a particular port:
```
show mac address-table dynamic interface fastEthernet 0/1
```

Find the mac address table entries for one VLAN:
```
show mac address-table dynamic vlan 1
```

Aging timer setting for the switch:
```
show mac address-table aging-time
```

```
show mac address-table
```



### Port security ^8c754e
```
show port-security
```

```
show port-security address
```

```
show port-security interface f1/0/1
```

### EtherChannels
```
show etherchannel summary
```

```
show etherchannel 1 summary
```

```
show etherchannel 1 port-channel
```

```
show etherchannel load-balance
```
### Protocols
#### ARP
```
show arp
```

#### VTP
```
show vtp status
```

#### DTP
```
show dtp interface g0/0
``` 

#### CDP
```
show cdp neighbours
```

```
show cdp neighbours details
```

Disable CDP on an interface. (You want to disable CDP on interfaces that are facing outside you network for security reasons)
```
Router(config-if)#no cdp enable 
```

```
Router(config)no cdp run
```
