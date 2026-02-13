
## GRE Tunnel
To set up a GRE tunnel between these two offices, we first need to ensure they have reachability to each other's public interface IPs. In a GNS3 lab, you would typically have an "ISP" router in the middle acting as the gateways you've listed.

Here is the configuration to build the tunnel using the parameters you provided.

---

### 1. Basic Connectivity Check

Before building the tunnel, your routers must be able to ping across the "Internet."

- **OfficeA** must be able to ping `90.223.15.10`.
    
- **OfficeB** must be able to ping `90.223.15.6`.
    

---

### 2. GRE Tunnel Configuration

We will create a new virtual interface (**Tunnel 0**) and assign it a private internal network (let's use `10.0.0.0/30`).

#### OfficeA Configuration

Bash

```
interface GigabitEthernet0/0
 ip address 90.223.15.6 255.255.255.252
 no shutdown

# Default route to reach the "Internet"
ip route 0.0.0.0 0.0.0.0 90.223.15.5

# GRE Tunnel Setup
interface Tunnel0
 ip address 10.0.0.1 255.255.255.252
 tunnel source GigabitEthernet0/0
 tunnel destination 90.223.15.10
 # Optimization for GRE overhead
 ip mtu 1400
 ip tcp adjust-mss 1360
```

#### OfficeB Configuration

Bash

```
interface GigabitEthernet0/0
 ip address 90.223.15.10 255.255.255.252
 no shutdown

# Default route to reach the "Internet"
ip route 0.0.0.0 0.0.0.0 90.223.15.9

# GRE Tunnel Setup
interface Tunnel0
 ip address 10.0.0.2 255.255.255.252
 tunnel source GigabitEthernet0/0
 tunnel destination 90.223.15.6
 # Optimization for GRE overhead
 ip mtu 1400
 ip tcp adjust-mss 1360
```

---

### 3. Verification

Once configured, run these commands to ensure the tunnel is up:

1. **`show ip interface brief`**: Tunnel0 should be `up/up`.
    
2. **`ping 10.0.0.2`** (from OfficeA): This tests that traffic is successfully being encapsulated in GRE and traveling across the public link.
    
3. **`show interface tunnel 0`**: Look for the "Tunnel source" and "destination" lines to confirm the mapping.
    

---


To prepare your tunnel for **IPsec**, we need to "over-provision" our MTU reduction. Since IPsec overhead varies slightly depending on the encryption algorithm (AES-128 vs. AES-256) and hashing (SHA-256 vs. SHA-512), we use a conservative estimate.

### The "Safety" Calculation

Here is the breakdown of the overhead we must account for:

- **Original IP MTU:** 1500 bytes
    
- **GRE Header:** 24 bytes (20-byte IP + 4-byte GRE)
    
- **IPsec ESP Header/Trailer:** ~56 bytes (Typical maximum for AES/SHA-256 in **Tunnel Mode**)
    
- **Total Overhead:** ~80 bytes
    

1500−80=1420

While **1420** is mathematically precise for many setups, the industry standard is to drop down to **1400** or **1424** to provide a "buffer" for additional headers (like MPLS labels or QinQ tags) that your ISP might add without your knowledge.


---

###  Why the TCP MSS is 1360

It is important to remember that `ip mtu` tells the **router** how to handle packets, but `ip tcp adjust-mss` tells the **endpoints** (the PCs) how to behave.

When a PC starts a TCP connection, it sends a SYN packet. The router sees this packet entering the tunnel, looks inside, and rewrites the "Maximum Segment Size" field. By setting it to **1360**, the PCs will never send a segment larger than that, ensuring the final packet (after IP, TCP, GRE, and IPsec headers are added) stays safely under **1500**.

---

## IPSec Tunnel

We need to configure two phases: **Phase 1 (ISAKMP)** to negotiate _how_ to talk, and **Phase 2 (IPsec)** to actually encrypt the data.

---

### Phase 1: ISAKMP (The Management Plane)

This defines the "handshake" parameters. Both sides must match.

#### OfficeA & OfficeB (Same on both)

Bash

```
crypto isakmp policy 10
 encryption aes 256
 hash sha256
 authentication pre-share
 group 14  # Diffie-Hellman Group (Group 14 is the minimum secure standard)
 lifetime 86400

# Set the password (Key). Use the remote public IP of the other router.
# For OfficeA: 
crypto isakmp key CISCO_PASS address 90.223.15.10
# For OfficeB:
crypto isakmp key CISCO_PASS address 90.223.15.6
```

---

### Phase 2: IPsec (The Data Plane)

This defines the actual encryption used for your GRE packets.

#### OfficeA & OfficeB (Same on both)

Bash

```
crypto ipsec transform-set MY_SET esp-aes 256 esp-sha256-hmac
 mode transport  # Use transport mode because GRE already provides the outer IP header
```

> **Pro-Tip:** Since GRE already adds an IP header, using **`mode transport`** saves 20 bytes of overhead compared to the default "tunnel mode."

---

### The "Link": Creating the IPsec Profile

Now we bundle Phase 2 into a profile that we can apply to the tunnel interface.

Bash

```
crypto ipsec profile IPSEC_OVER_GRE
 set transform-set MY_SET
```

---

### Applying to the Tunnel

Now we tell **Tunnel0** to protect itself using that profile. This is where the magic happens.

#### OfficeA & OfficeB

Bash

```
interface Tunnel0
 tunnel protection ipsec profile IPSEC_OVER_GRE
```

---

### Verification: Is it Encrypted?

If everything is correct, the tunnel should stay "Up/Up," but your pings are now encrypted. Use these two commands—they are the most important for troubleshooting:

1. **`show crypto isakmp sa`**: You should see **`QM_IDLE`**. This means Phase 1 is successful.
    
2. **`show crypto ipsec sa`**: Look for the "pkts encaps" and "pkts decaps" counters.
    
    - If you ping `10.0.0.2` and these numbers go up, your GRE traffic is being successfully encrypted.


