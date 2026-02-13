# Appliances
#GNS3 #Networking 

## Nexus (NX-OSv)
Activate Lisence - In config mode, run the following command:
```
license grace-period
```

## CSR1000v
How to enable NETCONF
```
! Change date and time
! This step is necessary for NETCONF to work on this GNS3 Appliance due
! to an issue caused by a ceritificate that expired in 2020
!
clock set 10:20:00 9 MAY 2019
!
conf t
!
! Create a user and password
username admin priv 15 secret cisco
!
! Create an enable password
enable secret cisco
!
! Configure SSH
ip domain name lab.gns3.local
crypto key generate rsa modulus 2048
ip ssh version 2
ip ssh authentication-retries 3
ip ssh timeout 120
!
! Enable SSH on the VTY lines
line vty 0 4
 transport input ssh
 login local
 exit
!
! Configure the interface from which the router will be accessed
int GigabitEthernet1
 ip add 10.0.0.254 255.255.255.0
 no shut
 exit
!
! Enable NETCONF
netconf-yang
!

```

Verify that NETCONF is running
```
show platform software yang-management process
```


How to enable RESTCONF
```
conf t
! Create a user and password
username admin priv 15 secret cisco

!Enable HTTP Server
ip http secure-server

! Enable the RESTCONF server
restconf
```

Test
```
curl -k https://10.0.0.254/restconf/ -u "admin:cisco"
```

---

## Toolbox
### Rsyslog
#### 1. Enable UDP syslog reception

Edit the rsyslog config:
`sudo nano /etc/rsyslog.conf`

Uncomment (or add) these lines:

```
module(load="imudp") 
input(type="imudp" port="514")
```

👉 This tells rsyslog to **listen on UDP/514**.

---

#### 2 (Optional but recommended) Create a log file for router logs

Create a custom config file:

`sudo nano /etc/rsyslog.d/10-router.conf`

Example rule:
```
# Cisco router logs
local7.*    /var/log/cisco.log
& stop
```

Replace `192.168.1.1` with **R1’s IP address**.

---

#### 3. Restart rsyslog

```
service restart rsyslog
```

---

#### 4 Verify rsyslog is listening

```
sudo ss -lunp | grep 514
```

You should see rsyslog bound to UDP/514.

---

### SNMP manager

#### Configure `snmpd` (agent on Toolbox – optional but useful)

This allows **R1 or the Ubuntu client to query the Toolbox**, useful for testing.

**Edit config*
```
sudo nano /etc/snmp/snmpd.conf
```
Replace the file contents with something **simple and lab-safe**:

```
# Listen on all interfaces 
agentAddress udp:161  

# Read-only community 
rocommunity public 192.168.27.0/24  

# System info 
sysLocation GNS3-Lab 
sysContact admin@lab.local
```

Restart:

```
sudo systemctl restart snmpd
```

Test locally:

```
snmpwalk -v2c -c public 127.0.0.1 sysDescr
```

---

#### Configure SNMP Trap Receiver (`snmptrapd`)

This is the **most important part** for router labs.

**Edit config**

```
sudo nano /etc/snmp/snmptrapd.conf
```

Minimal working config:

```
# Allow SNMPv2c traps 
authCommunity log,execute,net public

# Log traps to syslog 
logOption f
```

Restart:

```
sudo systemctl restart snmptrapd
```

Verify it is listening:

```
sudo ss -lunp | grep 162
```

---

#### Run snmptrapd in foreground (for learning)

This is **extremely useful in labs**:

```
sudo snmptrapd -f -Lo
```

You’ll see traps immediately on the console.

(Stop with `Ctrl+C` after testing.)

#### Configure SNMP on R1 (Cisco IOS)

```
conf t  
snmp-server community public RO  
snmp-server location GNS3-Lab  
snmp-server contact admin@lab.local  exit
```

Verify:

`show snmp`

---

## 6. Configure R1 to send traps to Toolbox

`conf t  snmp-server host 192.168.27.10 version 2c public  snmp-server enable traps  exit`

This enables **all standard traps**.

---

## 7. (Recommended) Enable specific trap types

For labs, these are gold:

`conf t  snmp-server enable traps snmp linkdown linkup  snmp-server enable traps config  snmp-server enable traps syslog  exit`

---

# PART 4 — Test the setup

## 8. Test SNMP polling (from Toolbox → R1)

From the Toolbox:

`snmpwalk -v2c -c public 192.168.27.254 sysName`

You should see:

`SNMPv2-MIB::sysName.0 = STRING: R1`

---

## 9. Test SNMP traps (best test)

On R1:

`interface GigabitEthernet0/1  shutdown  no shutdown`

On Toolbox (foreground mode):

`sudo snmptrapd -f -Lo`

You should see `linkDown` and `linkUp` traps immediately.

---

## 10. Where traps are logged (background mode)

If running as a service, traps go to:

`/var/log/syslog`

You can filter:

`grep snmp /var/log/syslog`