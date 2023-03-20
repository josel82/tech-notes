# Useful commands
#Linux #Commands #Networking 

## nslookup
```bash
nslookup <domain name>
```
Will return the IP address of a given domain name. E.g.:

```bash
┌──[18:45:47]─[0]─[raspberrypi:~]
└──| nslookup brady.ns.cloudflare.com
Server: 10.10.0.1
Address: 10.10.0.1#53
  
Non-authoritative answer:
Name: brady.ns.cloudflare.com
Address: 162.159.44.215
Name: brady.ns.cloudflare.com
Address: 108.162.195.215
Name: brady.ns.cloudflare.com
Address: 172.64.35.215
Name: brady.ns.cloudflare.com
Address: 2803:f800:50::6ca2:c3d7
Name: brady.ns.cloudflare.com
Address: 2a06:98c1:50::ac40:23d7
Name: brady.ns.cloudflare.com
Address: 2606:4700:58::a29f:2cd7
```

if not installed you can do so in debian distribuitions with:

```bash
sudo apt install dnsutils
```

## dig
```bash
dig <IP Address>
```
Utility for checking if a domain name record has been propagated across the internet