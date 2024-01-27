# DHCP Snooping

## Enabling DHCP snooping on a L2 Switch
On Global Configuration mode:
```
ip dhcp snooping
ip dhcp snooping vlan [number]
no ip dhcp snooping information option
```

The reason for the `no ip dhcp snooping information option` is that DHCP relay agents add new fields to the DHCP requests (defined as option 82 DHCP header field). Switches add this option to this messages by default, and that works fine in L3 switches that are being used as DHCP relay agents, but because in this case we are configuring a Layer 2 switch (which cannot act as DHCP relay agent), we need to disable this feature or else DHCP request messages will get discarded by the DHCP relay agents.

### Setting switch port as a trusted port
On Interface configuration mode:
```
ip dhcp snooping trust
```

### Limiting DHCP message rates
This is sent on a per interface basis. On interface config mode:
```
ip dhcp snooping limit rate [number]
```
\[number] as in packets per second

if the rate of DHCP messages surpasses the set limit, the switch will put the interface in error disabled mode. It will require to `shutdown/no shutdown` the interface in order to bring it back up. We can make this action less severe by enabling error recovery globally.
On global config mode:
```
errdisable recovery cause dhcp-rate-limit
errdisable recovery interval [number]
```
\[number] seconds

## Show commands
```
show ip dhcp snooping
```