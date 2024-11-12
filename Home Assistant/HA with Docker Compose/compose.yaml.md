
You can create a new folder in your home directory and copy the following docker compose file
`compose.yaml`
```yaml
version: "3"
services:
  homeassistant:
    container_name: homeassistant
    image: "ghcr.io/home-assistant/home-assistant:stable"
    volumes:
      - /opt/stacks/hass/hass-config:/config
      - /etc/localtime:/etc/localtime:ro
      - /run/dbus:/run/dbus:ro
    devices:
    # Make sure this matched your adapter location
      - /dev/ttyUSB0:/dev/ttyUSB0
    restart: unless-stopped
    privileged: true
    network_mode: host

  nodered:
    container_name: nodered
    image: nodered/node-red
    ports:
      - 1880:1880
    volumes:
      - /opt/stacks/hass/nodered:/data
    depends_on:
      - homeassistant
      - mosquitto
    environment:
      - TZ=Europe/Dublin
    restart: unless-stopped

  mosquitto:
    image: eclipse-mosquitto
    container_name: mosquitto
    restart: unless-stopped
    ports:
      - 1883:1883
      - 9001:9001
    volumes:
      - /opt/stacks/mosquitto/config:/mosquitto/config
      - /opt/stacks/mosquitto/data:/mosquitto/data
      - /opt/stacks/hass/mosquitto/log:/mosquitto/log
    environment:
      - TZ=Europe/Dublin
    user: "${PUID}:${PGID}"

  hass-configurator:
    image: causticlab/hass-configurator-docker:latest
    restart: always
    ports:
      - 3218:3218/tcp
    volumes:
      - /opt/stacks/hass/configurator-config:/config
      - /opt/stacks/hass/hass-config:/hass-config

  portainer:
    container_name: portainer
    image: portainer/portainer-ce
    restart: always
    ports:
      - "9000:9000/tcp"
    environment:
      - TZ=Europe/Dublin
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /opt/stacks/portainer:/data

  zigbee2mqtt:
    container_name: zigbee2mqtt
    image: koenkk/zigbee2mqtt
    restart: unless-stopped
    volumes:
      - /opt/stacks/hass/zigbee2mqtt/data:/app/data
      - /run/udev:/run/udev:ro
    ports:
      # Frontend port
      - 8080:8080
    environment:
      - TZ=Europe/Dublin
    devices:
      # Make sure this matched your adapter location
      - /dev/serial/by-id/usb-Nabu_Casa_SkyConnect_v1.0_a6ed5d63af57ed11be0b4aca5720eef3-if00-port0:/dev/ttyUSB0
```


