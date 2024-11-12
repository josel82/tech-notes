# vpn-setup

In this example I am using NordVPN as my VPN provider. Prior running the following commands, I have downloaded a server configuration file from NordVPN (UDP) and copied it on to openWRT as `/etc/openvpn/client.conf`

Now I can proceed with the following steps
## Install packages

```bash
opk update
opkg install luci-app-openvpn
/etc/init.d/rpcd restart
```
  
  

## Configuration parameters
replace the values of `OVPN_USER` and `OVPN_PASS` with your NordVPN credentials
```bash
OVPN_DIR="/etc/openvpn"
OVPN_ID="client"
OVPN_USER="USERNAME"
OVPN_PASS="PASSWORD"
```


## Save username/password credentials

```bash
umask go=
cat << EOF >${OVPN_DIR}/${OVPN_ID}.auth
${OVPN_USER}
${OVPN_PASS}
EOF
```

  

## Configure VPN service

```bash
sed -i -e "
/^auth-user-pass/s/^/#/
\$a auth-user-pass ${OVPN_ID}.auth
/^redirect-gateway/s/^/#/
\$a redirect-gateway def1 ipv6
" ${OVPN_DIR}/${OVPN_ID}.conf
/etc/init.d/openvpn restart
```
  

## provide VPN instance management

```bash
ls /etc/openvpn/*.conf \
| while read -r OVPN_CONF
do
OVPN_ID="$(basename ${OVPN_CONF%.*} | sed -e "s/\W/_/g")"
uci -q delete openvpn.${OVPN_ID}
uci set openvpn.${OVPN_ID}="openvpn"
uci set openvpn.${OVPN_ID}.enabled="1"
uci set openvpn.${OVPN_ID}.config="${OVPN_CONF}"
done
uci commit openvpn
/etc/init.d/openvpn restart
```
  
  

## Configure firewall

```bash
uci rename firewall.@zone[0]="lan"
uci rename firewall.@zone[1]="wan"
uci del_list firewall.wan.device="tun+"
uci add_list firewall.wan.device="tun+"
uci commit firewall
/etc/init.d/firewall restart
```
  

## Configure hotplug

```bash
mkdir -p /etc/hotplug.d/online
cat << "EOF" > /etc/hotplug.d/online/00-openvpn
/etc/init.d/openvpn restart
EOF
cat << "EOF" > /etc/sysupgrade.conf
/etc/hotplug.d/online/00-openvpn
EOF
```
