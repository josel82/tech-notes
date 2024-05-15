# AAA Docker container appliance


It consists of a Ubuntu docker container. It comes with `tac_plus` and `freeradius`. It runs the `tac_plus` deamon by default. The `freeradius` server needs to be started:

```
service freeradius start
```

This radius server listens on udp ports 1812 and 1813 for authentication and accounting respectively.

### Adding Radius user

Add the following lines on top of the `/etc/freeradius/3.0/mods-config/files/authorize` file:

```
myUsername  Cleartext-Password := "pass123"
            Reply-Message = "Hello, %{User-Name}"

```

Save the file and restart the service:
```
service freeradius restart
```

## Tacacs+ Server
For instructions on how to configure the Tacacs+ server, read this tutorial [[Tutorials#Tac_plus]]


