# nmap

All this commands will work on a linux environment with nmap installed
## Scanning network
1. Know your Default gateway
```
route
```
2. know your IP address
```
ifconfig
```


## L2 scan
```
nmap -PR -ns 10.0.2.0/24
```


save all found IP address in a text file:
```
nano iplist.txt
```
*iplist.txt*
```
10.0.2.10
10.0.2.14
10.0.2.15
10.0.2.50
10.0.2.254
```

## L3 scan
```
sudo nmap -PE -sn [x.x.x.x/x | URL]
```

## L4 scan
```
sudo nmap -PA[port] -sn [x.x.x.x/x | URL]
```

## Port scanning
Search for open ports in an specific host
```
nmap x.x.x.x 
```

Search for open ports in a list of hosts
```
nmap -iL iplist.txt
```

Search for a specific port in a list of hosts
```
nmap -p [port] -iL iplist.txt
```



