[Source](https://github.com/ChristianLempa/videos/tree/main/teleport-tutorial)

[[Installing Docker Engine in Ubuntu]]

Create a virtual machine with Docker Engine and docker-compose installed 
Create a new directory `/opt/teleport`. In there create a `docker-compose.yaml` file with the following config:
```yaml
version: '2'
services:
  configure:
    image: quay.io/gravitational/teleport:4.3
    container_name: teleport-configure
    entrypoint: /bin/sh
    hostname: fully.qualified.domain
    command: -c "if [ ! -f /etc/teleport/teleport.yaml ]; then teleport configure > /etc/teleport/teleport.yaml; fi"
    volumes:
      - ./config:/etc/teleport

  teleport:
    image: quay.io/gravitational/teleport:4.3
    container_name: teleport
    entrypoint: /bin/sh
    hostname: fully.qualified.domain
    command: -c "sleep 1 && /bin/dumb-init teleport start -c /etc/teleport/teleport.yaml"
    ports:
      - "3023:3023"
      - "3024:3024"
      - "3025:3025"
      - "3080:3080"
    volumes:
      - ./config:/etc/teleport
      - ./data:/var/lib/teleport
    depends_on:
      - configure
```

Then run docker-compose:
```bash
docker-compose up -d
```

This will generate, configuration files, set up volumes etc. Once this is done we can then modify the `docker-compose.yaml` file as follows:
```yaml
version: '2'
services:
  teleport:
    image: quay.io/gravitational/teleport:4.3
    container_name: teleport
    entrypoint: /bin/sh
    hostname: fully.qualified.domain
    command: -c "sleep 1 && /bin/dumb-init teleport start -c /etc/teleport/teleport.yaml"
    ports:
      - "3023:3023"
      - "3024:3024"
      - "3025:3025"
      - "3080:3080"
    volumes:
      - ./config:/etc/teleport
      - ./data:/var/lib/teleport
```

This is because we no longer need the "configure" container.

Open `/opt/teleport/config/teleport.yaml` it should look something like this
```yaml
#
# Sample Teleport configuration file
# Creates a single proxy, auth and node server.
#
# Things to update:
# 1. ca_pin: Obtain the CA pin hash for joining more nodes by running 'tctl status'
# on the auth server once Teleport is running.
# 2. license-if-using-teleport-enterprise.pem: If you are an Enterprise customer,
# obtain this from https://dashboard.gravitational.com/web/
#
teleport:
	nodename: teleport
	data_dir: /var/lib/teleport
	auth_token: 429810fa82891fe8ec76ec14940b7b39991277f391b712d7
	auth_servers:
	- 127.0.0.1:3025
	log:
		output: stderr
		severity: INFO
	ca_pin: sha256:ca-pin-hash-goes-here
auth_service:
	enabled: "yes"
	listen_addr: 0.0.0.0:3025
	tokens:
	- proxy,node:429810fa82891fe8ec76ec14940b7b39991277f391b712d7
	license_file: /path/to/license-if-using-teleport-enterprise.pem
ssh_service:
	enabled: "yes"
	labels:
	db_role: master
	db_type: postgres
	commands:
	- name: hostname
	command: [/usr/bin/hostname]
	period: 1m0s
	- name: arch
	command: [/usr/bin/uname, -p]
	period: 1h0m0s
proxy_service:
	enabled: "yes"
	listen_addr: 0.0.0.0:3023
	web_listen_addr: 0.0.0.0:3080
	tunnel_listen_addr: 0.0.0.0:3024
```

Make sure you add `public_addr:<fqdm>` under the `auth_service` section ot the `teleport.yaml`
```yaml
auth_service:
	enabled: "yes"
	listen_addr: 0.0.0.0:3025
	public_addr: fully.qualified.domain:3025
	tokens:
	- proxy,node:429810fa82891fe8ec76ec14940b7b39991277f391b712d7
	license_file: /path/to/license-if-using-teleport-enterprise.pem
```

Also add `public_add:<fqdm>` and `ssh_public_addr:<fqdm>` under `proxy_service`
```yaml
proxy_service:
	enabled: "yes"
	listen_addr: 0.0.0.0:3023
	public_addr: fully.qualified.domain
	ssh_public_addr: fully.qualified.domain
	web_listen_addr: 0.0.0.0:3080
	tunnel_listen_addr: 0.0.0.0:3024
```

Now, run the following command:
```bash
docker-compose up -d --force-recreate --remove-orphans
```

Then obtain the certificate pin hash:
```bash
docker-compose exec teleport tctl status
```

Grab the hash and paste it onto `ca_pin` value under the `teleport` service

Add users:
```bash
docker-compose exec teleport tctl users add teleport root,tomc,brucel
```
