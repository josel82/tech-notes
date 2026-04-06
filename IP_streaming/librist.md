# librist

## Setting up Ubuntu VM for RIST streaming

### Update packages
```bash
sudo apt-get update && sudo apt-get upgrade -y
```

### Install Linux Build Essentials
```bash
sudo apt install -y build-essential meson ninja-build pkg-config \\
git libmbedtls-dev libmicrohttpd-dev libcjson-dev
```

### Clone RIST repository
From the home directory run:
```bash
git clone <http://code.videolan.org/rist/librist.git>
cd librist
rm -rf build # Start clean
```

### Compile the Library
```bash
#Configure the build 
meson setup build -Dtest=true -Dbuilt_tools=true -Dbuiltin_mbedtls=true
```

```bash
ninja -C build
sudo ninja -C build install
sudo ldconfig  # Refresh the library cache
```

### Verify installation
```bash
sudo ldconfig
ristsender --help
ristsender --help-url
```

### Install ffmpeg
```bash
sudo apt-get install ffmpeg -y
```

## Testing the library
**📋 Quick Reference Table**

| **Protocol URL**       | **Symbol**   | **Meaning**                        | **Role**             |
| ---------------------- | ------------ | ---------------------------------- | -------------------- |
| `udp://1.2.3.4:5000`   | **No `@`**   | Send data **to** 1.2.3.4           | Transmitter (Client) |
| `udp://@1.2.3.4:5000`  | **With `@`** | Listen on **my** IP 1.2.3.4        | Receiver (Server)    |
| `rist://@0.0.0.0:8200` | **With `@`** | Listen on **all** my network cards | Server/Listener      |

1. Setup a UDP stream (`ffmpeg` test pattern) from the VM to Macbook
```bash
ffmpeg -re \\
  -f lavfi -i testsrc=d=65585:s=1920x1080:r=23.97,format=yuv420p \\
  -f lavfi -i sine=f=440:b=4 \\
  -shortest \\
  -mpegts_flags resend_headers \\
  -muxrate 10M \\
  -max_interleave_delta 0 \\
  -f mpegts \\
  "udp://<macbook-ip>:8194?pkt_size=1316&buffer_size=65535"

```

2. At the macbook, play the udp stream either with VLC or with `ffplay`
```bash
ffplay -i 'udp://<macbook-ip>:8194'
```

3. UDP stream to localhost for `ristsender` to send
```bash
ffmpeg -re \\
-f lavfi -i testsrc=d=65585:s=1920x1080:r=25,format=yuv420p \\
-f lavfi -i sine=f=440:b=4 \\
-shortest \\
-c:a aac -b:a 192k \\
-f mpegts \\
"udp://127.0.0.1:8196?pkt_size=1316&buffer_size=65535"
```

4. Setup Multi-User Authorisations
```bash
ristsrppasswd josepadilla pass123 > /tmp/ristpasswords.txt
ristsrppasswd bobmarley pass456 >> /tmp/ristpasswords.txt
ristsrppasswd jimihendrix pass789 >> /tmp/ristpasswords.txt
```

5. Setup and run the `ristsender` command
```bash
ristsender -p 1 -e 128 \\
-s pass123 -F /tmp/ristpasswords.txt \\
-i "udp://@127.0.0.1:8196?stream-id=8196" \\
-o "rist://@10.1.10.65:8196?cname=VM201&bandwidth=25000&buffer=2000&rtt-min=60&rtt-max=500"
```

6. At the macbook, 10.1.20.119
```bash
ristreceiver -p 1 -e 128 \\
-s pass123 \\
-i "rist://10.1.10.65:8196?bandwidth=25000&buffer=2000&rtt-min=60&rtt-max=500&username=josepadilla&password=pass123" \\
-o "udp://127.0.0.1:8198?stream-id=8196"
```

Note: UDP stream-id have to match on both sender and receiver
```bash
ffplay -i 'udp://127.0.0.1:8198?stream-id=8196'
```

## Streaming a file (mpeg-ts ove udp)
```bash
ffmpeg -re \\
-i my-video.mp4 \\
-c:v copy \\
-c:a aac -b:a 192k \\
-f mpegts \\
"udp://127.0.0.1:8196?pkt_size=1316&buffer_size=65535"

```

## RIST Relay workflow

Relay Server
```bash
rist2rist -p 1 \\
  -i "rist://@0.0.0.0:8196?bandwidth=25000&buffer=2000&aes-type=128&secret=pass123" \\
  -o "rist://@0.0.0.0:8296?bandwidth=25000&buffer=2000&aes-type=128&secret=pass123"
```

`librist` tools have two ways to set these values:

1. **Global Flags:** Using `p`, `e`, and `s` at the start of the command applies those settings to **all** connections in that command.
2. **URL Parameters:** Using `?aes-type=128&secret=pass123` inside the quotes allows you to have **different** settings for different inputs or outputs.

In your current `rist2rist` relay, using the **URL parameters** is safer because it explicitly tells the relay exactly how to handle that specific "listening" port.

Sender (Host A)
```bash
ristsender -p 1 -e 128 -s pass123 \\
  -i "udp://@127.0.0.1:8196" \\
  -o "rist://<RELAY-IP>:8196?bandwidth=25000&buffer=2000"
```

Receiver (Host B)
```bash
ristreceiver -p 1 -e 128 -s pass123 \\
  -i "rist://<RELAY-IP>:8296?bandwidth=25000&buffer=2000" \\
  -o "udp://127.0.0.1:8198"
```

## RIST Command Flag Breakdown

### `p` (Profile)
This flag tells the library which version or "level" of the RIST protocol to use.

- **`p 0` (Simple Profile):** This is the original version of RIST. It focuses purely on packet recovery (ARQ). It does **not** support encryption or complex authentication.
- **`p 1` (Main Profile):** This is what you are using now. It is built on top of the Simple Profile but adds support for **encryption**, GRE tunneling (which allows multiple streams over one port), and more advanced congestion control.

### `e` (Encryption Type)
This flag specifies the bit-length of the **AES (Advanced Encryption Standard)** encryption.

- **Value:** Usually set to `128` or `256`.
- **Requirement:** Encryption is a feature of the **Main Profile**. If you try to use `e` with `p 0`, the command will usually fail or ignore the encryption.
- **Performance:** 128-bit is generally faster and uses less CPU, while 256-bit is more secure but slightly more "expensive" in terms of processing power.

### `s` (Secret / Passphrase)
This is your **Shared Secret**. It is the password that the RIST engine uses to encrypt the data packets.

- **Consistency:** For the stream to work, the Sender, Relay, and Receiver must all have the **exact same string** following the `s` flag.
- **Security:** This is what turns your AES-128 or AES-256 encryption "on." Without the correct secret, a receiver will see the traffic arriving but will be unable to decode the video.