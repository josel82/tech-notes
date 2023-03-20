# Systemd
#Linux 

[systemd](https://en.wikipedia.org/wiki/Systemd) is asoftware suite that provides an array of system components forLinux operating systems. The main aim is to unify service configuration and behavior acrossLinux distributions.

In Linux, services are called "units".

## Managing Service Units

- Checking unit status
```bash
sudo systemctl status apache2
```

- Checking global status
```bash
sudo systemctl status
```

- Listing units
```bash
systemctl list-unit-files --type=service
```

- Disabling a unit
```bash
sudo systemctl disable apache2
```
Disabling a unit won't stop a service, disabling means that the unit won't start automatically next time the system restarts.

- Stopping a unit
```bash
sudo systemctl stop apache2
```

-  Enabling a unit
```bash
sudo systemctl enable apache2
```
By enabling the unit you are telling the system to start the service next time the system restarts.

- Starting a unit
```bash
sudo systemctl start apache2
```

- Restarting a unit
```bash
sudo systemctl restart apache2
```
This command is often used to restart a unit after some configuration has been changed

-  Reloading a unit
```bash
sudo systemctl reload apache2
```
This command is preferred over `restart` when possible, because `reload` would not stop the service.