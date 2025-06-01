# SNMP examples



## Example 1

```
# SNMP v2c on Cisco device

# Optional
snmp-server contact admin@example.com
snmp-server location network lab

# Communities
snmp-server community public ro
snmp-server community private rw

# SNMP server
snmp-server host 10.1.1.10 version 2c community public
# In this example we have chosen "public" as the community for connection with  # the NMS. The NMS will only be allow to read information. The private community
# is not used.

# Configuring Traps
snmp-server enable traps snmp linkdown linkup
snmp-server enable traps config
```



## Example 2


```
# Simple SNMP v3 configuration

snmp-server view ALL-ACCESS iso included
snmp-server group ADMIN v3 priv read ALL-ACCESS
snmp-server user JOSE ADMIN v3 auth sha pass123 priv des56 asdfasdf
```