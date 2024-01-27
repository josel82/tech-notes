# DHCPD docker image

1. Build a docker image inside the GNS3 VM.
2. On the GNS3 client go to `preferences/Docker/Docker containers/new` 
3. Select the image from the dropdown menu
4. follow the instructions

Dockerfile location (GNS3 VM) `/home/gns3/dhcp`

```
FROM ubuntu:focal

RUN apt update && apt upgrade -y
RUN apt install isc-dhcp-server -y

WORKDIR /home/gns3/dhcp
COPY ./config/dhcpd.conf /etc/dhcp/dhcpd.conf

RUN touch /var/lib/dhcp/dhcpd.leases
#CMD ["/usr/sbin/dhcpd", "-4", "-f", "-d", "--no-pid", "-cf", "/etc/dhcp/dhcpd.conf"]
```

For this server to work, we need to declare the network its interface is on in the config file.

dhcpd.conf
```
# No service will be given on this subnet, but declaring it helps the
# DHCP server to understand the network topology.

subnet 172.17.0.0 netmask 255.255.0.0 {
}
```

So basically, according to the current build, we would need to rebuild the docker image every time we want to assign an ip address of a network is not declared in the latest config file.


server start command:
```
/usr/sbin/dhcpd -4 -f -d --no-pid -cf /etc/dhcp/dhcpd.conf
```