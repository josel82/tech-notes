# Keeping upgrades up to date

## Manually
```bash
sudo apt update && sudo apt dist-upgrade -y
```

## Automatically
```bash
sudo apt update
sudo apt install unattended-upgrades -y
sudo dpkg-reconfigure --priority=low unattended-upgrades
#Follow the prompt
```
