# DHCP Snooping
#CISCO #CyberSecurity #EthicalHacking

DHCP snooping is a security technology on a Layer 2 network switch that can prevent unauthorized DHCP servers from accessing your network. It is a protection from the untrusted hosts that want to become DHCP servers. DHCP Snooping works as a protection from man-in-the-middle attacks [1](https://en.wikipedia.org/wiki/DHCP_snooping)[2](https://www.ionos.com/digitalguide/server/security/dhcp-snooping/).

## Enable DHCP Snooping Globally
In global configuration mode run:
```cisco
ip dhcp snooping
```

## Enable DHCP Snooping on a VLAN
In global configuration mode run:
```cisco
ip dhcp snooping vlan 1
```

## Disable DHCP Snooping option 82
In global configuration mode run:
```cisco
no dhcp snooping information option 
```

## Configure a trusted port
Run the following command:
```cisco
int g0/0
ip dhcp snooping trust
exit
```

## Rate limit untrusted ports
This helps with preventin DOS attacks by limiting the amount of packets per second an untrusted port can send. If a device violates this rate, the port will be error disabled.

Run the following command:
```cisco
int g0/1
ip dhcp snooping limit rate 10
exit
```
In this example we have set the rate limit to 10 dhcp packets per second

## Show commands

^ecd92e

In  privilege mode run:
```cisco
show ip dhcp snooping
```

```cisco
show ip dhcp binding
```

^d84648

