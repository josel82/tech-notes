# Port scanning

## NMAP
### Ping scan
```bash
nmap -sn 192.168.1.0/24
```
Saving the output to a file:
```bash
nmap -sn 192.168.1.0/24 -oN subnet_scan.txt
```
Scanning for open ports:
```bash
nmap -sS 192.168.1.0/24
```