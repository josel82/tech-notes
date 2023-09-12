# Gathering information about your system
#Proxmox #Virtualization #Linux #Debian

## CPU information

```bash
lscpu
```

## Hardware information
```bash
lshw
```
Chances are that the first time you run this command it won't be available on your system. In that case you can install it as follows:

Update the repository
```bash
apt update -y && apt upgrade -y
```

```bash
apt install lshw -y
```


another option is running:
```bash
dmidecode -t [option]
```

```
dmidecode: option requires an argument -- 't' 
Type number or keyword expected 
Valid type keywords are: 
  bios 
  system 
  baseboard 
  chassis 
  processor 
  memory 
  cache c
  onnector 
  slot
```

If your system doesn't have `dmidecode` command you can install it as follows:
```bash
apt install dmidecode -y
```
# Firmware information
```bash
dmidecode -t bios
```