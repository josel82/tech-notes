[Documentation](https://goteleport.com/blog/letsencrypt-teleport-ssh/)

Follow the instructions in the documentation above. Make sure you add `/etc/letsencrypt:/etc/letsencrypt` volume in the `docker-compose.yaml` file.

```yaml
version: '2'
services:
	teleport:
	image: quay.io/gravitational/teleport:4.3
	container_name: fullt.qualified.domain
	entrypoint: /bin/sh
	hostname: fullt.qualified.domain
	command: -c "sleep 1 && /bin/dumb-init teleport start -c /etc/teleport/teleport.yaml"
	ports:
	- "3023:3023"
	- "3024:3024"
	- "3025:3025"
	- "3080:3080"
	volumes:
	- ./config:/etc/teleport
	- ./data:/var/lib/teleport
	- /etc/letsencrypt:/etc/letsencrypt
```