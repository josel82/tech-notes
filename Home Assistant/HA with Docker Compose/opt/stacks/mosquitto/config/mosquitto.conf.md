```
persistence true
persistence_location /mosquitto/data/
log_dest file /mosquitto/log/mosquitto.log
listener 1883
listener 9001

## Authentication ##
allow_anonymous false
password_file /mosquitto/config/password.txt
```