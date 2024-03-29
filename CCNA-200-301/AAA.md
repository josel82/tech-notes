# AAA
#CISCO #CCNA 

## The Three levels of Authentication (AAA)
- **Authentication** - the process of verifying the user's identity.
- **Authorisation** - the process of verifying the level of access configured for a user.
- **Accounting** - the process of recording the use of resources.
## Authentication Factors
The three authentication factors are something you know, something you have and something you are.
1. Password, PIN
2. Code Generator Device, smart card, etc.
3. Finger print, retina reader, etc.
Multifactor authentication refers to the use of two or three factors to authenticate a user.
Therefore, dual-factor authentication is also sometimes known as multifactor authentication.

## 802.11 MAC Frame Format

| FC | DUR | ADD1 | ADD2 | ADD3 | SEQ | ADD4 | DATA | FCS |
|---|---|---|---|---|---|---|---|---|
| 2bytes | 2bytes | 6bytes | 6bytes | 6bytes | 2bytes | 6bytes | Var | 4bytes |

FC = Frame Control
DUR = Duration
ADD1 = Address 1
ADD2 = Address 2
ADD3 = Address 3
SEQ = Sequence
ADD4 = Address 4
DATA = Contains the frame's payload
FSC = Frame Check Sequence 

## Protocols 

| Protocol | TCP | UDP | Port |
|---|---|---|---|
| Syslog | no | yes | 514 |
| Syslog | yes | no | 1468 |
| NTP | no | yes | 123 |
| TFTP | no | yes | 69 |
| SNMP | no | yes | 161/162 |

## DTP (Dynamic Trunk Protocol)
There are two dynamic modes of operation for a switch port:
- **auto** - operates in access mode unless the neighbouring interface actively negotiates to operates as a trunk
- **desirable** - operates in access mode unless it can actively negotiate a trunk connection with a neighbouring interface. 

## Cyber Security

### Attacks
- **MAC Spoofing attack** - an attacker uses another known host on the network in order to bypass port security measures. MAC Spoofing can also be used to impersonate another host on the network. Implementing sticky secure MAC addresses can help mitigate MAC Spoofing attacks.
- **MAC Flooding attack** - an attacker generates thousands of forged frames every minute with the intention of overwhelming the switch's mac address table. Once the table is flooded, the switch can no longer make intelligent forwarding decisions and all traffic is flooded. This allows the attacker to view all data sent through the switch because all traffic will be sent out each port.
- **ARP poisoning attack** - 
- **VLAN hoping attack** - 
- **DHCP spoofing attack** - 