# Networks
#Docker #DevOps #Networking 

## Default Docker Bridge

It requires containers to map ports that need to be exposed outside, such as ports 80, 443, etc. All containers for which we don't specify any network run on this network. Containers can communicate with each other with their IP addresses but they cannot do DNS name resolution or container isolation. Default bridge are not ideal for applications when one container needs to communicate with a database because the connection has to be made with the DB's IP and this may change after a container restart.  For this type of situations it is advisable to use User Defined Bridges.

Example:

The following command will create a nginx container and connect it to the docker0 bridge by default:
```bash
docker run --rm -d --name nginx -p 80:80 nginx
```

![default-docker-bridge.png](../Images/default-docker-bridge.png)


## User Defined Bridge

Meant for container isolation. Containers can communicate with other containers inside the same bridge and can do so using DNS name resolution.  Inbound and outbound traffic is NATed. Ports need to be exposed.

Example:

Here we are attaching a container to a user defined bridge that was previously created:
```bash
docker network create custom_bridge
```

```bash
docker run --rm --network custome_bridge --name nginx -p 80:80 nginx
```

![user-def-bridge.png](../Images/user-def-bridge.png)


## Overlay

This is for inter host container communication over Layer 2.

![overlay.png](../Images/overlay.png)


## Host Driver

This is used for cases where container isolation is not the goal. We will use the Host Driver in cases where our container requires access to resources running in the host network. A container running with the Host Driver is analogous to an application running directly in the host. In this case a container would not need to expose its ports.

Examples:

```bash
docker run --rm --network host --name nginx  nginx
```
or
```yaml
version: '3'
services:
  web-server:
    image: nginx
    volumes:
	    - ./templates:/etc/nginx/templates
    environment:
	    - NGINX_HOST=foobar.com
	    - NGINX_PORT=80
    network_mode: host
```

## Macvlan

You would want to use this driver to run a container that exposes a port that is already in use on the Host. Here we bridge our containers to the host physical network, but with a different MAC address. Containers don't need to expose ports.

You create a macvlan as follows:
```bash
docker network create -d macvlan --subnet 192.168.0.0/24 --gateway 192.168.0.1 --ip-range 192.168.0.253/32 -o parent=ens18 custom-macvlan
```

-   Same subnet and gateway as the Docker Host
-   We pass the --ip-range argument and assign an IP that I know it's not in use in the Host Network. This is because Docker's internal DHCP would try to give the container the first IP address available within the subnet we specify and this may cause conflict with other devices in the Host Network. Then  Make sure to exclude that IP address from the pool on the Host Network DHCP server
-   We also specify the parent interface we are bridging the macvlan to. In this example 'ens18' is the Host physical interface
-   Finally assign the macvlan a custom name

After we have created the macvlan, we can then run a container in it:
```bash
docker run --name netshoot --rm -it --network custom-macvlan nicolaka/netshoot /bin/bash
```

If I wanted to run another container in the same network it won't let me because the IP range we pass had only one IP address but we can still run other containers using static IP address:

```bash
docker run --name netshoot --rm -it --ip 192.168.0.200 --network custom-macvlan nicolaka/netshoot /bin/bash
```

```bash
docker run --name netshoot --rm -it --ip 192.168.0.201 --network custom-macvlan nicolaka/netshoot /bin/bash
```

**SOLUTION**: In case you run into connection problems, here is a solution:`

On the host run:
```bash
sudo ip link set <interface name> promisc on
```

E.g:
```bash
sudo ip link set enp0s3 promisc on
```
You may need to restart the host for this to work


### MacVlan Subnet

You create a subnet as follows:

```bash
docker network create -d macvlan --subnet 192.168.0.0/24 --gateway 192.168.0.1 --ip-range 192.168.0.253/32 -o parent=ens18.20 new-macvlan
```
Pay close attention to the ".20" added at the end of the host's interface. This tells Docker that you intend to create a new sub-interface


## IPvlan

Very similar to Macvlan but in this case you would get different IP addresses assigned to one MAC address. This type of driver is used in a case when a specific switch doesn't like different MAC addresses on one port and starts dropping packages for that reason. In this very specific case switching to IPvlan would solve the problem.

L2 Mode
```bash
docker network create -d ipvlan --subnet 192.168.0.0/24 --gateway 192.168.0.1 --ip-range 192.168.0.253/32 -o parent=ens18 custom-ipvlan
```


## Creating a Docker Network

```bash
docker network create <network-name>
```
Attach running containers to the Docker Network

In the following example we will be connecting a mongoDB container to a mongo-express cointainer:
1. Start the mongoDB container
```bash
docker run -d
-p 27017:27017 \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=password \
--network mongo-network \
--name mongodb \
mongo
```

2. Start the mongo-express container
```bash
docker run -d \
-p 8081:8081  \
-e ME_CONFIG_MONGODB_SERVER=mongodb  \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
--network mongo-network \
--name mongo-express \
mongo-express
```
Containers use their container names to communicate with each other within a Docker Network
