# RIST Labs

12 Dec 2025

Tested a RIST connection between **ubuntu-streamer** and **Jose’s Macbook**

**Kiloview Encoder → mpegts → ubuntu-streamer → RIST → (Tailscale VPN) → RIST → Jose’s Macbook**

### Kiloview Encoder

pushing mpegts to: `udp://239.1.1.10:5100`

### ubuntu-streamer
```bash
ristsender -p 1 -e 128 \\
-s pass123 -F /tmp/ristpasswords.txt \\
-i "udp://239.1.1.10:5100?stream-id=8196" \\
-o "rist://@10.1.10.65:8196?cname=VM201&bandwidth=10000&buffer-min=500&buffer-max=500&rtt-min=30&rtt-max=100&reorder-buffer=20&virt-dst-port=1969&weight=0&congestion-control=1"
```

### Macbook
```bash
ristreceiver -p 1 -e 128 \\
-s pass123 \\
-i "rist://10.1.10.65:8196?bandwidth=10000&buffer-min=500&buffer-max=500&rtt-min=30&rtt-max=100&reorder-buffer=20&virt-dst-port=1968&weight=0&congestion-control=1&username=josepadilla&password=pass123" \\
-o "udp://127.0.0.1:8198?stream-id=8196"
```

### **Results**

Glitching on the video. It looked like an payload issue rather than RIST

Test pattern generated locally with ffmpeg on ubuntu-streamer, and streamed with the same RIST connection, plays without glitches on my macbook

Bundleling

Host A

Terminal 1

```bash
ffmpeg -re \\
-f lavfi -i testsrc=d=65585:s=1920x1080:r=25,format=yuv420p \\
-f lavfi -i sine=f=440:b=4 \\
-shortest \\
-c:a aac -b:a 192k \\
-f mpegts \\
"udp://127.0.0.1:8196?pkt_size=1316&buffer_size=65535"
```

Terminal 2

```bash
ristsender -p 1 -e 128 \\
-s pass123 \\
-i "udp://@127.0.0.1:8196?stream-id=5000" \\
-o "rist://10.1.10.66:6000?bandwidth=20000&buffer=2000&virt-dst-port=1001"
```

```bash
ristsender -p 1 -e 128 \\
-s pass123 \\
-i "udp://@239.1.1.10:5100?stream-id=5002" \\
-o "rist://10.1.10.66:6000?bandwidth=20000&buffer=2000&virt-dst-port=1002"
```

Relay

```bash
rist2rist -p 1 \\
  -i "rist://@0.0.0.0:6000?bandwidth=40000&buffer=2000&aes-type=128&secret=pass123" \\
  -o "rist://@0.0.0.0:6001?bandwidth=40000&buffer=2000&aes-type=128&secret=pass123"
```

Receiver Termina 1

```bash
ristreceiver -p 1 -e 128 \\
-s pass123 \\
-i "rist://10.1.10.66:6001?bandwidth=20000&buffer=2000&virt-dst-port=1001" \\
-o "udp://127.0.0.1:8198?stream-id=5000"
```

```bash
ristreceiver -p 1 -e 128 \\
-s pass123 \\
-i "rist://10.1.10.66:6001?bandwidth=20000&buffer=2000&virt-dst-port=1002" \\
-o "udp://127.0.0.1:8199?stream-id=5002"
```

```bash
 ristsender -p 1 -e 128 \\
 -s pass123 \\
 -i "udp://@127.0.0.1:5100?stream-id=1000" \\
 -i "udp://@239.1.1.10:5100?stream-id=1002" \\
 -o "rist://@0.0.0.0:6000"
```

```bash
ristreceiver -p 1 -e 128 \\
-s pass123 \\
-i "rist://10.1.20.65:6000?virt-dst-port=1000" \\
-o "udp://127.0.0.1:6001"
```

```bash
 ristsender -p 1 -e 128 \\
 -s pass123 \\
 -i "udp://@239.1.1.10:5100?stream-id=1000" \\
 -i "udp://@127.0.0.1:5100?stream-id=1002" \\
 -o "rist://@0.0.0.0:6000"
```

```bash
ristreceiver -p 1 -e 128 \\
-s pass123 \\
-i "rist://10.1.20.65:6000?virt-dst-port=1000" \\
-o "udp://127.0.0.1:6001"
```

```bash
ristsender -p 1 -e 128 \\
-s pass123 \\
-i "udp://@239.1.1.10:5100?cname=stream01&stream-id=2,udp://@127.0.0.1:5100?cname=02&stream-id=4" \\
-o "rist://@0.0.0.0:6000"
```

Latest try

```bash
ffmpeg -re \\
-f lavfi -i testsrc=d=65585:s=1920x1080:r=25,format=yuv420p \\
-f lavfi -i sine=f=440:b=4 \\
-shortest \\
-c:a aac -b:a 192k \\
-f mpegts \\
-muxrate 6M \\
"udp://127.0.0.1:5101?pkt_size=1316&buffer_size=65535"
```

```bash
 ristsender -p 1 -e 128 \\
 -s pass123 \\
 -i "udp://@127.0.0.1:5101?stream-id=2,udp://@239.1.1.10:5100?miface=ens19&stream-id=4" \\
 -o "rist://100.122.33.21:6000?buffer=1000&bandwidth=30000"
```

```bash
ristreceiver -p 1 -e 128 \\
-s pass123 \\
-i "rist://@100.122.33.21:6000?buffer=1000&bandwidth=30000" \\
-o "udp://127.0.0.1:6001?stream-id=2,udp://127.0.0.1:6002?stream-id=4"
```

### Testing multiplex 20251226-2030

```bash
ffmpeg -re \\
-f lavfi -i testsrc=d=65585:s=1920x1080:r=25,format=yuv420p \\
-f lavfi -i sine=f=440:b=4 \\
-shortest \\
-c:v libx264 -preset ultrafast -tune zerolatency -b:v 2500k \\
-c:a aac -b:a 128k \\
-f mpegts -muxrate 3M \\
"udp://127.0.0.1:8192?pkt_size=1316&buffer_size=65535"
```

```bash
ristsender -p 1 -e 128 \\
-s pass123 \\
-i 'udp://@127.0.0.1:8192?&stream-id=1000,udp://@239.1.1.10:5100?miface=ens19&stream-id=2000' \\
-o 'rist://100.122.33.21:8200?cname=SENDER01&bandwidth=15000&buffer=2000&congestion-control=1'
```

```bash
ristsender -p 1 -e 128 \\
-s pass123 \\
-i "udp://@127.0.0.1:8192?stream-id=1000&multiplex-mode=1,udp://@239.1.1.10:5100?miface=ens19&stream-id=2000&multiplex-mode=1" \\
-o "rist://100.122.33.21:8200?cname=SENDER01&bandwidth=15000&buffer=2000&congestion-control=1"
```

```bash
ristreceiver -p 1 -e 128 \\
-s pass123 \\
-i 'rist://@100.122.33.21:8200?cname=RECEIVER01&bandwidth=15000&buffer=2000&congestion-control=1' \\
-o 'udp://127.0.0.1:6000?stream-id=1000,udp://127.0.0.1:6100?stream-id=2000'
```

Results: I get `Sender queue is full` error

---

### Testing Link 20251226-2225

Remote link across the internet - connected with Tailscale

TX: ubuntu-streamer

RX: macbook

Results:

RTT min/avg/max/mdev = 34.162/54.006/144.081/31.119 ms

Jitter min/max = 0.453/4.451 ms

Bandwidth:

Ideal 15Mbps

Starts dropping packets at 20Mbps

Gets really bad at 30Mbps

test

sender

```bash
ristsender -p 1 -e 128 \\
-s pass123 \\
-i "udp://@239.1.1.10:5100?miface=enp1s0f0&stream-id=2,udp://@127.0.0.1:5101?stream-id=4" \\
-o "rist://10.1.20.190:8200?buffer=25&bandwidth=20000"
```

receiver

```bash
ristreceiver -p 1 -e 128 \\
-s pass123 \\
-i "rist://@10.1.20.190:8200?buffer=25&bandwidth=20000" \\
-o "udp://127.0.0.1:6001?stream-id=2,udp://127.0.0.1:6002?stream-id=4"
```