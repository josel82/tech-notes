# SNMP v3 configuration

```
snmp-server view ALL-ACCESS iso included
snmp-server group ADMIN v3 priv read ALL-ACCESS
snmp-server user JOSE ADMIN v3 auth sha pass123 priv des56 asdfasdf
```