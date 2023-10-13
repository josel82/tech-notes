## Ping from a specific interface
```
Router# ping <dest IP address> source <src IP address>
```
E.g.
```
Router# ping 192.168.0.1 source 192.168.2.1
Router# ping 2001:1:1::1 source 2001:1:1:2:1
Router# ping 192.168.0.1 repeat 100
````

## Enabling logging
```
Router#term mon
```
Also
```
Router(config)#logging console
```
to disable
```
Router(config)#no logging console
```

## Configuring Interfaces
Enter to interface configuration mode (from global configuration mode)
```
SW1(config)#interface fastEthernet 0/1
```
### Set duplex
```
SW1(config-if)#duplex auto|half|full
```
### Set speed
```
SW1(config-if)#speed auto|10|100|1000
```
### Description
```
SW1(config-if)#description Printer on 3rd floor, Preset to 100/full
```

## Selecting multiple interfaces
```
SW1(config)#interface range fastEthernet 0/11 - 20
```

## Disabling VTP
It is recommended disabling VTP in Lab environment to avoid undesired behaviour caused by VTP.
```
SW1(config)#vtp mode off
```

## Interfaces to default config
```
SW1(config)#default interface g0/1
```

range of interfaces
```
SW1(config)#default interface range g0/1 - 3
```


## History
Lists the commands currently held in the history
```
show history
```

This command allows a single user to set, just for this one login session, the size of their history buffer
```
terminal history size x
```

From console or vty config mode. sets the default number of commands saved in the history buffer for the users of the console or vty, respectively
```
history size x
```

## Console Timeout
```
R1(config-line)#exec-timeout <minutes> <seconds>
```

Never time out:
```
R1(config-line)#exec-timeout 0 0
```

## Enabling linux commands on Cisco IOS
Feature available from Cisco IOS Release 15.1M
### Terminal option
This option enables the Linux shell but only for the current terminal session.
```
Router#terminal shell
Router#terminal shell trace
```
To disable
```
Router#terminal no shell
```

### Configuration Option (Recommended)
```
Router(config)#shell processing full
```
To disable
```
Router(config)#no shell processing
```

Shows all available commands on this shell
```
Router#show shell functions
```

Once enabled, you can run linux commands such as nested grep:
```
Router#sh ip int brief | grep up | grep -v 172 | grep -v 192 | grep -v loop
```

Other useful linux commands
- Get information about the device
```
Router#uname -a
```

- Man pages of a command
```
Router#man <command>
```

- Safe output into a file and store it in flash:
```
Router#sh run > shrun.cfg
```

- read file using cat command:
```
Router#cat shrun.cfg
```


# Delete configuration

This command erases the startup-config file
```
Router#erase startup-config
```

This command deletes
```
Router#delete vlan.dat
```

## Clear MAC address table

```
Router#clear mac address-table dynamic
```

Only clear mac addresses in VLAN 1:
```
Router#clear mac address-table dynamic vlan 1
```

Clear mac addresses learned from a particular interface:
```
Router#clear mac address-table dynamic interface fastEtherner 0/1
```

Remove a specific mac address from the table:
```
Router#clear mac address-table dynamic address 0201.1111.1111
```

