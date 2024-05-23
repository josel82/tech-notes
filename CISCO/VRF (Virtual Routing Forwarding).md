# VRF (Virtual Routing Forwarding)

It divides routers up into different routing tables. Similar concept to VLANs but for routers and L3 switches. 

## Configuration
In global configuration mode, the following commands create two new VRFs:
```
ip vrf VRF1
ip vrf VRF2
```
Next, int interface config mode, the following command configure a given interface to a specific VRF:
```
int g0/0
  ip vrf forwarding VRF1
  ip add 192.168.0.1 255.255.255.0
  no shutdown
  exit

int g0/1
  ip vrf forwarding VRF1
  ip add 192.168.1.1 255.255.255.0
  no shutdown
  exit
```
In the example above, we have configured interfaces GigabitEthernet 0/0 and GigabitEthernet 0/1 in the Same VRF, VRF1.

```
int g1/0
  ip vrf forwarding VRF2
  ip add 192.168.10.1 255.255.255.0
  no shutdown
  exit

int g1/1
  ip vrf forwarding VRF2
  ip add 192.168.1.1 255.255.255.0
  no shutdown
  end
```
Then we have configured interfaces GigabitEthernet 1/0 and GigabitEthernet 1/1 int VRF2. Notice that interface GigabitEthernet 1/1 is configured with the same IP address and in the same subnet as in interface GigabitEthernet 0/1. Normally, a router would not allow this, because the interfaces would be overlapped, but because the interfaces are in different VRF they are not in the same routing table, therefore it is not a problem.


## Show commands
```
show ip vrf
show ip route vrf VRF1
```

## PINGing with VRF
When VRF is configured, we need to add the following to the ping command in order for it to work:
```
ping vrf VRF1 192.168.0.2
```