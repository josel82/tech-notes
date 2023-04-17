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
iwconfig wlan0 mode monitor
```

```bash
ifconfig wlan0 up
```

## Check if it works
```bash
ifconfig
```

```bash
airodump-ng wlan0
```

```bash
airplay-ng --test wlan0
```