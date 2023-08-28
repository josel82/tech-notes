Types:

- IEEE 802.1D Legacy standard of spaning tree. It was developed for bridges. Very slow.
	- CST (Common Spanning Tree) Assumes the there is on Spanning Tree instance for the entire bridged network.

- PVST (Per VLAN Spanning Tree) Only supported ISL encapsulation

- PVST+ Supports ISL and 802.1Q encapsulation. This are Cisco enhancement of Spanning Tree that provides 802.1Q Spanning Tree instances for every VLAN. This means that if I had 100 VLANs I would end up having a 100 instances of Spanning Tree, all with their onw root and sending their own BPDUs.

- MSPT (Multiple Spanning Tree) It optimizes PVST by mapping multiple VLANs to the same Spanning Tree instance. For example, if you had 20 VLANs you could have 10 VLANs mapped to one instance of Spanning Tree and the other 10 to another instance.

- RSPT (Rapid Spanning Tree) Improves the convergance of the old version of Spanning Tree by:
	- giving roles to ports
	- enhancing BPDU exchanges
	This version of Spanning Tree has a much quicker convergence but only supports a single instance of Spanning Tree
	MSPT has RSPT built in.

- Rapid PVST+  Cisco has developed this version of PVST which provides quicker convergence but only supports a single instance of Spanning Tree.

So, The rule of thumb is: if you are setting up a network with a number of about 10 VLANs, use Rapid PVST+. But if you are dealing with a larger deployment with around 100 VLANs MSPT would be a more suitable version of Spanning Tree

#### Root Bridge
The switch with the lowest bridge ID in the topology becomes the Root Bridge.
In the past the bridge ID consisted of:
**Bridge ID: 8 Bytes**
| Bridge Priority | MAC Address |
|:---:|:---:|
| 2 Bytes | 6 Bytes |

Now in
**PVST+Extended Bridge ID: 8Bytes**
The Bridge priority is splited into two:

| Bridge Priority | Extended System ID | MAC Address |
|:---:|:---:| :---:|
| 4 bits | 12 bits | 6 Bytes |
| value you can set (32768 default)| VLAN # | MAC Address |

The first 4 bits of the 16 bits number are related to the bridge Priority.
0000 0000 0000 0000 = 0
0001 0000 0000 0000 = 4096
0010 0000 0000 0000 = 8192
0011 0000 0000 0000 = 12228
This means that only values that are multples of 4096 are allowed as Bridge priority 
 

#### Root ports
Once a Root Bridge is elected the remaining switches will designate their root ports. This will be the port with the lowest cost to get to the root bridge. Any other ports connected to the root will be in a blocking state. Root ports are elected primarily by their cost, but port priority and port numbers are used as tie breakers.

#### Path Cost

| Ethernet Speed | IEEE Cost 1998 (and before) | IEEE Cost 2004 (and after) |
|---|---:|---:|
| 10 Mbps | 100 | 2,000,000 |
| 100 Mbps | 19 | 200,000 |
| 1 Gbps | 4 | 20,000 |
| 10 Gbps | 2 | 2,000 |
| 100 Gbps | N/A | 200 |
| 1 Tbps | N/A | 20 |



You can configure a switch to use the IEEE Cost 2004 with the following command
`SW1(config)#spanning-tree pathcost method long`

#### How to designate a switch as the root switch
Assuming we are running PVST, you can designate a switch as the root switch of VLAN 1 as follows:
`SW2(config)#spanning-tree vlan 1 root primary`

#### How to change spanning tree mode
`SW2(config)#spanning-tree mode pvst`

#### Some **show** commands
`SW1#show spanning-tree` provides information relatied to spanning tree
`SW1#show spanning-tree interface gigabitEthernet 0/0 cost` gives you the path cost to the root switch from that port
`SW1#show spanning tree root`  It gives information that help identiy the root switch and root port on a switch