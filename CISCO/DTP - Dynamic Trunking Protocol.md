Protocol used by switched to negotiate link modes. 
Switch ports are configured to operate in Dynamic Auto mode by default when DTP is enabled, but you can set them to Dynamic Desirable if you want a port to try to negotiate a trunk on a link.

**Administrative Mode:** dynamic auto / dynamic desirable
**Operational Mode:** static access / static trunk
**Administrative Trunking Encapsulation:** negotiate / ISL / 802.1q

**Show commands**
`SW1#show interface g0/0 switchport`
`SW1#show dtp interface g0/0`
`SW1#show interfaces trunk`

Switch ports are confired as Dynamic Auto by default.

#### Setting up DTP as dynamic desirable on an interface
```
SW1(config)#int g0/0
SW1(config-if)#switchport mode dynamic desirable
```

DTP negotiation
| | Dynamic Auto | Dynamic Desirable | Trunk | Access |
|---|---|---|---|---|
| Dynamic Auto | Access | Trunk | Trunk | Access |
| Dynamic Desirable | Trunk | Trunk | Trunk | Access |
| Trunk | Trunk | Trunk | Trunk | Limited Connectivity |
| Access | Access | Access | Limited Connectivity | Access |

A switchport has to either be manually configured as an access or trunk port or automatically with DTP

#### How to disable DTP
First configure the port manually as either Access or Trunk, then declare  `switchport nonegotiate`

```
SW1(config)#int g0/1
SW1(config-if)#switchport mode access
SW1(config)#switchport nonegotiate
```

```
SW1(config)#int g0/0
SW1(config-if)#switchport trunk encapsulation dot1q
SW1(config-if)#switchport mode trunk
SW1(config-if)#switchport nonegotiate
```

### Note:
For security reasons, it is recomended to configure switch ports manually and to disable DTP 