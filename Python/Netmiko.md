# Netmiko
#Python #SSH #Networking 

Python library for connecting to multivendor network devices via SSH
[Documentation:](https://github.com/ktbyers/netmiko)

## Installation
```bash
pip install netmiko
```

## How to use it in python scripts
```python
from netmiko import ConnectHandler

#Device diccionary
cisco_IOSvl2 = {
    'device_type': 'cisco_ios',
    'host':   '10.1.1.1',
    'username': 'admin',
    'password': 'cisco',
    'port' : 8022,          # optional, defaults to 22
    'secret': 'secret',     # optional, defaults to ''
}

#Establish SSH connection with device from the diccionary
net_connect = ConnectHandler(**cisco_IOSvl2)

#Execute show command
output = net_connect.send_command('show ip int brief')
print(output)

```

## Config commands
```python
#Execute config commads
config_commands = [ 'int loop 0',
                    'ip add 1.1.1.1 255.255.255.255',
                    'no shut' ]
output = net_connect.send_config_set(config_commands)
print(output)
```

## Using a For Loop
```python
#For loop
for n in range(2,21):
   config_commands = [ 'vlan ' + str(n),
                       'name Vlan ' + str(n)]
   output = net_connect.send_config_set(config_commands)
   print(output)
```