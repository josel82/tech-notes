# OpenVSwitch commands
#OpenVSwitch

## Show commands
### Bridges and interfaces info
```
ovs-vsctl show
```

### Available Flows in the OpenFlow Table 
```
ovs-ofctl -O OpenFlow13 dump-flows br0
```

### Available Ports
```
ovs-ofctl -O OpenFlow13 dump-ports br0
```

## Enable Spanning Tree
```
ovs-vsctl set bridge br0 stp_enable=true
```

## Set controller
```
ovs-vsctl set-controller br0 tcp:<controllers-ip>:6633
```

## Troubleshooting 
OpenVSwitch does no connect to OpenDayLight Controller
```
ovs-vsctl set bridge br0 protocols=OpenFlow13
```