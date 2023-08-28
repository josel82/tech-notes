##### Ping from a specific interface
`Router# ping <dest IP address> source <src IP address>`
E.g.
`Router# ping 192.168.0.1 source 192.168.2.1`
`Router# ping 2001:1:1::1 source 2001:1:1:2:1`
`Router# ping 192.168.0.1 repeat 100` 

##### Enabling logging
`Router#term mon`
Also
`Router(config)#logging console`
to disable
`Router(config)#no logging console`