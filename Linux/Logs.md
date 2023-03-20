# Logs
#Linux #Logs

Log files live in the `/var/log` directory

## Hardware and kernel info
```bash
cat /var/log/dmesg
```

## Output dmesg logs in a nicer way
```bash
sudo dmesg
```

## System logs
```bash
cat /var/log/syslog
```
useful commands for reading logs [[Data Streams#^910172]]


## Journalctl 

Journalctl is part of Systemd
```bash
journalctl -u <unit_name>
```
Shows logs of an specific unit.

- Example 1
```bash
journalctl -u apache2
```

- Example 2
```bash
journalctl -fu apache2
```
Shows logs and follows.