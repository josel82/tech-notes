# Useful commands

### Show routes
```bash
netstat -rn
```

### Show specific routes
```bash
route get <destination IP>
```

### Flushing the routing table
```
sudo route -n flush
```

### Show DNS resolvers
```
scutil --dns
```

### Flush DNS cache
```
sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder
```