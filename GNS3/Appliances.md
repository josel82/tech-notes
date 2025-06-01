# Appliances
#GNS3 #Networking 

## Nexus (NX-OSv)
Activate Lisence - In config mode, run the following command:
```
license grace-period
```

# CSR1000v
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