[Cheat sheet](file:///Users/josepadilla/Documents/CiscoLearning/IOS_IPv4_Access_Lists.pdf)

#### Standard Access List
`  Router(config)#access list <1 - 99> <permint | deny | > <IP | any | host>`
e.g.
```cisco
Router#conf t
Router(config)#access-list 1 permit 10.1.1.1
```
This access list will only allow the host with IP 10.1.1.1

#### How to bind an access list to an interface
`  Router(config)#access-group <access list #> <in | out>`
e.g.
```cisco
Router(config)#int f0/0
Router(config)#access-group 1 in
```
In this example we are binding the previous access list to interface fastEthernet 0/0 against inbound packets. Here, only packages that match the IP 10.1.1.1 will be allow in through interface f0/0.

#### How to bind an access list to VTY lines
```cisco
Router#conf t
Router(config)#access list 10 permit 10.1.1.1
Router(config)#line vty 0 4
Router(config-line)#access-class 10 in
```
This will only allow the host with IP 10.1.1.1 to telnet or ssh to the router

#### Remarks
```cisco
Router#conf t
Router(config)#access-list 5 permit 10.1.2.1
Router(config)#access-list 5 remark Allows Admin to server
```

#### Extended Access List
`Router(config)#access-list <number> <action> <protocol> <src IP> <wild card> <dest IP> <port>`
e.g.
```cisco
Router#conf t
Router(config)#access-list 100 permit tcp 10.1.1.1 0.0.0.0 host 10.1.2.10 eq 80
Router(config)#access-list 100 deny ip 10.1.1.0 0.0.0.255 host 10.1.2.10
Router(config)#access-list 100 permit ip 10.1.1.0 0.0.0.255 any
Router(config)#int f0/0
Router(config-if)#ip access-group 100 in
```
The first statement allows the host 10.1.1.1 to send HTTP traffic to host 10.1.2.10
The second statement deny all other traffic from subnet 10.1.1.0/24 to host 10.1.2.10
The third statement allows all traffic to any other destinatination
Finally we bind the Extended ACL to an interface

#### How to edit ACLs
```cisco
Router(config)#ip access-list extended 100
Router(config-ext-nacl)#no 30
```
Here we have removed statement #30. Run a `show access-lists` before editing so you can see the number of the statement you intend to remove.

```cisco
Router(config-ext-nacl)#30 deny ip any host 10.1.2.10
```
You can also add a new statement to the ACL

#### Allow established connection
```cisco
Router(config)#access-list 101 permit tcp any 10.1.2.0 0.0.0.255 established
```
This statement allow packages comming from outside network 10.1.2.0/24 only if the communication had been stablished by a host withing the network

#### Deny explicitly for logging
```cisco
Router(config)#access-list 101 deny ip any 10.1.2.0 0.0.0.255 log
```
Deny is implicit, but we can use a statement like this for logging purposes


#### Guidelines

- Standard Access Lists - Filter on source IP Address
- Extended Access Lists - Filter on src/dest IP Addresses | src/dst ports | other options
- Staments are processed from top to bottom. Place more specific staments first.
- Deny all is implicit
- You can only bind one access list 
	- per interface
	- per direction (in/out)
	- per protocol
- If you bind a ACL to an interface that already has a ACL the later will be overwriten
- Place Standard ACLs as close to the destionation as possible
- Place Extended ACLs as close to de source as possible



