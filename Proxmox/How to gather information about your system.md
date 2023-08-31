# How to gather information about your system
#Proxmox #Virtualization #Linux #Debian

## Hardware information

```bash
lscpu
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