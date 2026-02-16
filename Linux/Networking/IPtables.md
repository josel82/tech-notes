# IPTables

## Basic rules for a server

```bash
# Flush existing rules (USE WITH CAUTION - WILL WIPE ALL CURRENT RULES)
# sudo iptables -F
# sudo iptables -X

# Set default policies (often set to DROP for INPUT for security)
# sudo iptables -P INPUT DROP
# sudo iptables -P FORWARD DROP
# sudo iptables -P OUTPUT ACCEPT

# Allow loopback traffic
sudo iptables -A INPUT -i lo -j ACCEPT
sudo iptables -A OUTPUT -o lo -j ACCEPT

# Allow established and related connections (crucial for replies)
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# Allow SSH (TCP port 22)
sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW -j ACCEPT

# Optional: Allow HTTP/HTTPS if it's a web server
# sudo iptables -A INPUT -p tcp --dport 80 -m state --state NEW -j ACCEPT
# sudo iptables -A INPUT -p tcp --dport 443 -m state --state NEW -j ACCEPT

# Optional: Allow Ping (ICMP)
# sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT

# Drop all other incoming traffic (if default policy is ACCEPT)
# This rule should be at the very end of your INPUT chain if your default is ACCEPT
# If your default is DROP, this is not strictly necessary but harmless.
# sudo iptables -A INPUT -j DROP
```

## Making Iptables rules persistent

For Debian/Ubuntu servers:

```bash
sudo apt-get install iptables-persistent
sudo netfilter-persistent save
```

or

```bash
sudo service netfilter-persistent save
```

## Verifying rules

```bash
sudo iptables -L -n -v
```

- `L`: Lists the rules.
- `n`: Shows numerical output (IPs instead of hostnames, ports instead of service names), which is faster.
- `v`: Provides verbose output (shows byte/packet counts).

Flushing rules

```bash
sudo iptables -F # Flushes all rules from all chains
sudo iptables -X # Deletes all non-default chains
sudo iptables -Z # Zeroes the packet and byte counters
```