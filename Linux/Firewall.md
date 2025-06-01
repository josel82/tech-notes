# Firewall
#Linux #iptables 

## Basic stateful firewall
```bash
#!/bin/bash


# We start by flushing any existing rules
iptables --flush

##Policies##
#
# We define a 'Drop everything' policy for the input chain.
iptables --policy INPUT DROP 
# We define an 'Accept everything' policy for the output chain.
iptables --policy OUTPUT ACCEPT
# We define a 'Drop everything' policy for the forward chain
iptables --policy FORWARD DROP

# Next we accept traffic in and out of the loopback interface
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT

# Here we define the stateful firewall
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

#Add custom rules below
```


```
#Commands
-A --append : Append to the end of the selected chain
-I --insert : Insert to chain at the specified pocition  
-L --list : List the current rules on the chain

#Parameters
-i --in-interface : to specify the interface the packet ingress
-o --out-interface : to specify the interface the packet egress
-j --jump : indicates what to do if the packet matched the rule
--policy : deafult policy on a chain
-m --match : specifies a match to use

#Action
DROP : Drops packets quietly
ACCEPT : Accept packets
REJECT : Drops packets and sends a 'Destination unreacheble' reply to the source of the packet

```

## Making rules permanent
The easiest way to make iptables rules permanent is by installing the iptables-permanent module. Run the following commands and follow the prompt.

```bash
sudo apt update
sudo apt install iptables-permanent
```