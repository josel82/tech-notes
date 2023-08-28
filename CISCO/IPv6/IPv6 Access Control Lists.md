In this example we create an ACL that will only permit traffic from 2001:1::/64 network and its applied to interface g0/0 inbound.
```cisco
R1#conf t
R1(config)#ipv6 access-list acl1
R1(config-ipv6-acl)#permit 2001:1::/64 any
R1(config-ipv6-acl)#int g0/0
R1(config-if)#ipv6 traffic-filter acl1 in
```

