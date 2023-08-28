#### Enable port security in switch port

```cisco
Switch#conf t
Switch(config)#int f0/0
Switch(config-if)#switchport port-security
```

This command will be rejected if the port is in "dynamic auto" mode (Dynamic Trunking Protocol). If so, set the port as an access port:

```cisco
Switch(config-if)#switchport mode access
Switch(config-if)#switchport port-security
```

Now port security should be enabled and you should be able to run:

```cisco
Switch#show port-security
```

By default this port would only allow one mac address which learns automatically. Other show commands: [[CISCO/Show commands#^8c754e]]


#### Port disabled
With port security enabled if the switch detects a mac address that's different from the one that had learned, it will error disable the port. You can get a report by running the following command:
```cisco
Switch#show port-security interface f0/0
```

#### Enable port
```cisco
Switch(config)#int f0/0
Switch(config-if)#shut
Switch(config)#no shut
```

#### Maximun Mac Addresses Allowed
```cisco
Switch(config)#int f0/0
Switch(config-if)#switchport port-security maximum 2
```
This command will set up the maximum number of mac addresses allowed to that port to two

#### Static Mode
```cisco
Switch(config-if)#switchport port-security mac-address 0023.3300.0000.0001
```

Sticky Mode
```cisco
Switch(config-if)#switchport port-security mac-address sticky
```
In this case the switch will learn a mac address dynamically and it will save it to the running configuration. 

#### Set action in case of violation
```cisco
Switch(config-if)#switchport port-security violation <action>
```
you can select between the following options:
- protect
- restric
- shutdown

#### Port security Error disable and auto recovery
```cisco
Switch(config)#errdisable recovery cause psecure-violation
Switch(config)#errdisable recovery interval 30
```