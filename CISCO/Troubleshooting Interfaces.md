# Troubleshooting Interfaces
#CISCO #Networking 


## Gather information about the link

The output below tells us the type of duplex and the speed of the link, and whether this values where automatically negotiated or manually configured. 
```
SW1#show interface gigabitEthernet 1/0/33

Port       Name          Status      Vlan        Duplex  Speed  Type
Gi1/0/33                 connected   1           a-full  a-100  10/100/1000BaseTX
```

The following command gives us more output. Here is a brief explanation of the different values:
```
show interface gigabitEthernet 1/0/33
```

**Runts**: Frames that did not meet the minimum frames size required (64bytes, including the 18-byte destination MAC, source MAC, type, and FSC). Can be caused by collisions.

**Giants**: Frames that exceed the maximum frame size requirement (1518 bytes, including the 18-byte destination MAC, source MAC, type, and FSC)

**Input Errors**: A total of many counters, including runts, giants, no buffer, CRC, frame, overrun, and ignored counts

**CRC**: Received frames that did not pass the FSC math; can be caused by collisions

**Frame**: Received frames that have an illegal format, for example, ending with partial byte; can be by collisions

**Packets Output**: Total number of packet (frames) forwarded out of the interface.

**Output errors**: Total number of packets (frames) that the switch port tried to transmit, but for which some problem occurred.

**Collisions**: Counter of all collisions that occur when the interface is transmitting a frame

**Late Collisions**: The subset of all collisions that happen after the 64th byte of the frame has been transmitted. (In a properly working Ethernet LAN, collisions should occur within the first 64 bytes; late collisions today often point to a duplex mismatch.)