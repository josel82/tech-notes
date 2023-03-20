# How to change DNS
#Linux #Networking

Some Linux distributions come with `systemd-resolved` which is systemd service unit for Network Name Resolution

In these cases, you can't change the DNS server just by editing the `/etc/resolv.conf` file. You can even read it on the file when you open it.

```
# This file is managed by man:systemd-resolved(8). Do not edit.
#
# This is a dynamic resolv.conf file for connecting local clients directly to
# all known uplink DNS servers. This file lists all configured search domains.
#
# Third party programs should typically not access this file directly, but only
# through the symlink at /etc/resolv.conf. To manage man:resolv.conf(5) in a
# different way, replace this symlink by a static file or a different symlink.
#
# See man:systemd-resolved.service(8) for details about the supported modes of
# operation for /etc/resolv.conf.
  
nameserver 192.168.0.33
search .
```

You can also see that `/etc/resolv.conf` points to another file when you run `ls /etc/`

![[resolv.conf.png]]

Which confirms that DNS settings are managed by `systemd-resolved.service`. Now, what exactly is the `systemd-resolved.service`? According to https://systemd.network/systemd-resolved.service.html, **systemd-resolved** is a system service that provides network name resolution to local applications. It implements a caching and validating DNS/DNSSEC stub resolver, as well as an LLMNR and MulticastDNS resolver and responder.

How can we change the DNS? 
We can change the DNS via the `resolvectl` API. https://www.man7.org/linux/man-pages/man1/resolvectl.1.html

First we find the link on which we want to make the change. In this example we want to change the DNS value on Link 2.
```
┌──[17:55:17]─[0]─[raspberrypi:~]
└──| resolvectl status
Global
       Protocols: +LLMNR +mDNS -DNSOverTLS DNSSEC=no/unsupported
resolv.conf mode: uplink
  
Link 2 (eth0)
Current Scopes: DNS LLMNR/IPv4
     Protocols: +DefaultRoute +LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
   DNS Servers: 192.168.0.33
  
Link 3 (wlan0)
Current Scopes: none
     Protocols: -DefaultRoute +LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  
Link 4 (br-3653ccaf0e42)
Current Scopes: LLMNR/IPv4 LLMNR/IPv6
     Protocols: -DefaultRoute +LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  
Link 5 (br-48cdbce3b7e3)
Current Scopes: LLMNR/IPv4 LLMNR/IPv6
     Protocols: -DefaultRoute +LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  
Link 6 (docker0)
Current Scopes: LLMNR/IPv4 LLMNR/IPv6
     Protocols: -DefaultRoute +LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported

```

```
┌──[17:56:31]─[0]─[raspberrypi:~]
└──| resolvectl status 2
Link 2 (eth0)
Current Scopes: DNS LLMNR/IPv4
     Protocols: +DefaultRoute +LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
   DNS Servers: 192.168.0.33
```

Next, we change the DNS value with the `dns` command, passing the Link number and IP address ass arguments. This commands requires root permissions.
```
┌──[17:57:46]─[0]─[raspberrypi:~]
└──| sudo resolvectl dns 2 192.168.0.1

┌──[17:58:00]─[0]─[raspberrypi:~]
└──| resolvectl status 2
Link 2 (eth0)
Current Scopes: DNS LLMNR/IPv4
     Protocols: +DefaultRoute +LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
   DNS Servers: 192.168.0.1
```