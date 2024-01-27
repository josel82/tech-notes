# WIFI Alfa AWUS036ACH
#Kali #Linux 

## Install driver
1. Connect the Wireless device to the Kali linux host.
2. Update package lists
```bash
sudo apt update
```
3. Install driver
```bash
sudo apt install realtek-rtl88xxau-dkms
```
4. Reboot the host

## Setup Wireless Adapter into Monitor Mode
```bash
airmon-ng check kill
```

```bash
airmon-ng start wlan0
```


## Check if it works
```bash
iwconfig
```

```bash
airodump-ng wlan0
```

```bash
airplay-ng --test wlan0
```

## Scan

```
airodump-ng wlan0 
```
By default it will scan only in 2.4Ghz

```
airodump-ng wlan0 --manufacturer
```
Gives you a bit more information

```
airodump-ng wlan0 --manufacturer --band abg
```
Scan in different bands
