#### Encaptulation HDLC
Layer 2 encaptulation for WAN links. Cisco has added an extra field to the header to differentiate among different types of higher level protocols such as IPv4, IPv6, CDP, etc. 
Here is how you enable HDLC on a cisco router:
```cisco
Router>enable
Router#conf t
Router(config)#int s0/0/0
Router(config-if)#ip add 10.22.1.2 255.255.255.252
Router(config-if)#encapsulation hdlc
Router(config-if)#no shut
```