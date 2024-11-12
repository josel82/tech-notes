```
homeassistant: true
permit_join: true
frontend: true
mqtt:
  base_topic: zigbee2mqtt
  server: mqtt://192.168.2.154
  user: hass
  password: 64Ks_NZuDFnn
serial:
  port: /dev/ttyUSB0
advanced:
  homeassistant_legacy_entity_attributes: false
  legacy_api: false
  legacy_availability_payload: false
device_options:
  legacy: false
```