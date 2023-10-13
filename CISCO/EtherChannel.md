# EtherChannel
#CISCO #Networking 

## Overview
In network topologies where there are multiple links between two switches, Spanning Tree Protocol (STP) will block all but one of the links in order to prevent loops. Etherchannel would take a group of links like the one described, and merge then into a logical port that would be seen by STP as one link, this way utilising all of the links, load balancing traffic across the two switches.

## Requirements
In order to participate in the Etherchannel, the configuration of the physical ports must be the same. Links which fail to this condition will remain configured as part of the Etherchannel but in a nonworking state.

Here is a list of parameters that the switch check when adding a link to an Etherchannel:
- Speed
- Duplex
- Operational access or trunking state (all must be access, or all must be trunks)
- If an access port, the access VLAN
- If a trunk port, the allowed VLAN list
- If a trunk port, the native VLAN
- STP interface settings

## Configuration
### Manual 
In interface configuration mode:
```
channel-group [1-225] mode on
```
Since this configuration doesn't involve negotiation, it has to be done on both sides of the link.

### Dynamic
#### LACP (Link Aggregation Control Protocol)
In interface configuration mode:
```
channel-group [1-225] mode [auto|desirable]
```
Mode 'auto' will passively wait for negotiation. Mode 'desirable' will actively negotiate an Etherchannel.

#### PAgP (Port Aggregation Protocol) 
In interface configuration mode:
```
channel-group [1-225] mode [passive|active]
```
Mode 'passive' will passively wait for negotiation. Mode 'active' will actively negotiate an Etherchannel.

### Load balancing
From global configuration mode:
```
port-channel load-balance [method] 
```

Methods:
- src-mac
- dst-mac
- src-dst-mac
- src-ip
- dst-ip
- src-dst-ip
- src-port
- dst-port
- src-dst-port

## Verifying Etherchannel

```
show etherchannel summary
```

```
show etherchannel 1 summary
```

```
show etherchannel 1 portchannel
```

```
show etherchannel load-balance
```

```
test etherchannel load-balance interface [channel-port] [mac|ip|port] [src] [dst]
```

ei.
```
test etherchannel load-balance interface po1 mac 0200.0000.0001 0200.1111.1111
test etherchannel load-balance interface po1 mac 0200.0000.0002 0200.1111.1111
test etherchannel load-balance interface po1 mac 0200.0000.0003 0200.1111.1111
```