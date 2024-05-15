# ASA

[Source material](https://youtube.com/playlist?list=PLsPPnwREYxwtt8VMft6sncz9D700W0Z3Y&si=mjeTVDX0fB2JlzZo)
## Basic configuration

### Inside interface
```
interface gigabitEthernet 0/0
nameif inside
ip address 192.168.1.1 255.255.255.0
no shutdown
```
Note: the `nameif inside` command sets the security level of the interface to 100
### Outside interface
```
interface gigabitEthernet 0/0
nameif outside
ip address 172.16.1.1 255.255.255.0
no shutdown
```
Note:  the `nameif inside` command sets the security level of the interface to 0

### DMZ interface
```
interface gigabitEthernet 0/0
security-level 50
nameif DMZ
ip address 10.1.1.1 255.255.255.0
no shutdown
```
For the DMZ we manually set the security level to 50

### Management interface
```
interface gigabitEthernet 0/0
security-level 80
nameif MGMT
ip address 172.21.1.1
no shutdown
```

## Routes
### Static route
```
route <Interface> <Dest-IP-Address> <Subnet-Mask> <Next-Hop-Address> <AD>
```

e.g.
```
route inside 2.2.2.2 255.255.255.255 192.168.1.2 10
```

### Default route
```
route <Interface> 0.0.0.0 0.0.0.0 <Next-Hop-Address> <AD>
```

e.g.
```
route outside 0.0.0.0 0.0.0.0 10.1.1.2 5
```

## Allow pings through
```
fixup protocol icmp
```

## Enabling HTTP
```
! Create a username and password
username admin password my_password encrypted privilege 15

! Enable HTTP server
http server enable

! Declare which network and which interface the server should
! expect http connections from
http 172.20.1.1 255.255.255.0 MGNT
```

## Enabling SSH
```
enable password my_enable_pass encrypted
username admin password my_password encrypted privilege 15
aaa authentication ssh console LOCAL
ssh 172.20.1.1 255.255.255.0 MGNT
domain-name lab.cisco.arpa 
crypto key generate rsa mode 4096
ssh version 2
ssh key-exchange group dh-group14-sha1
```

## Access Lists
```
access-list <ACL-Name> extended permit <protocol> <src-IP> <src-Mask> <dst-IP> <dest-mask>
```
e.g.
```
access-list OUTSIDE-DMZ extended permit icmp any host 10.1.50.100
```

### Apply the ACL
```
access-group OUTSIDE-DMZ in interface outside
```

## Object groups
- Protocol object group
- Network object group
- Service object group
- ICMP type object group

The following is an example of a network object:
```
object-group network OUTSIDE_LOOPBACKS
network-object host 10.10.10.1
network-object host 10.10.10.2
network-object host 10.10.10.3
network-object host 10.10.10.4
```

Next we have an example of a service object:
```
object-group service TELNET-HTTP tcp
port-object 23
port-object 80
port-object 443
```

Then we can simplify things, like a long ACL by using object groups like the ones above

```
access-list ALLOW-TCP extended permit tcp any object-group OUTSIDE_LOOPBACKS object-group TELNET-HTTP
```

Here is another example, this type we have an icmp-type object group:
```
object-group icmp-type ALLOW_PING
icmp-object echo
icmp-object echo-reply
```

And once again, we could use an object group like the one above in an access-list as follows:
```
access-list PING extended permit icmp any object-group OUTSIDE_LOOPBACKS object-group ALLOW_PING
```

## Static NAT
```
! create a network object for the host you want to do NAT on
object network Web-server
host 10.1.50.100 
! run the nat command as follows
nat (DMZ,outside) static 200.50.32.11 
```

## Setting up PAT (Overload)
```
! create a network object and declare the network 
! you want to do the NAT for
object network inside-LAN
subnet 192.168.1.0 255.255.255.0
! run the nat command as follows
nat (inside,outside) dynamic interface
```


## Show commands
```
show run policy-map global_policy

! NAT translations
show xlate
```


## Notes
- By default the firewall only allows traffic from a higher security lever to a lower security level.