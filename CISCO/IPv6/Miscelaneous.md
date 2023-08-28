
#### Test IPv6 connectivity
[Test IPv6 Here](http://test-ipv6.com)

### Hostnames 
```cisco
R1(config)#ipv6 host r2 2001:1:1:2::2
R1(config)#end
R1#ping r2
```


### Pings
Standard ping
```cisco
R1#ping 2001:FACE::1
```

Pingging from a specific interface
```cisco
R1#ping 2001:FACE::1 source loop 0
```

