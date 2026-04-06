# srt-tools package


## Installation

MacOS
```bash
brew install srt
```

Ubuntu
```bash
sudo apt install srt-tools
```

## Commands

Transmitter in **Listener** mode
```bash
srt-live-transmit \\
-loglevel:debug \\
"udp://@239.1.1.10:5100?rcvbuf=12000000" \\
"srt://:4242?mode=listener&latency=400&tos=184"
```

`-loglevel:debug` to get useful information for troubleshooting
`udp://@239.1.1.10:5100` **Input** - Binding to multicast mpegts stream
`srt://:4242` **Output** - Listening on all interfaces
## Receiver in **Caller** mode
```bash
srt-live-transmit \\
-loglevel:debug \\
"srt://10.1.10.65:4242?mode=caller&latency=400" \\
"udp://127.0.0.1:5100?pkt_size=1316"
```

`-loglevel:debug` to get useful information for troubleshooting
`srt://10.1.10.65:4242` **Input** - pointing to the IP address of the Listener
`udp://127.0.0.1:5100` Output - pushing the mpegts stream to localhost:5100

## Video Playout

On VLC
Go to **File → Open Network**
URL: `udp://@127.0.0.1:5100`
## Rendezvous Mode

### Transmitter
```bash
srt-live-transmit udp://@239.1.1.10:5100 \\
"srt://100.122.33.21:4242?mode=rendezvous&latency=200"

```
`100.122.33.21` Macbook’s IP address (Tailscale Tailscale)

### Receiver
```bash
srt-live-transmit \\
"srt://100.104.218.118:4242?mode=rendezvous&latency=200" \\
udp://127.0.0.1:5100
```
`100.104.218.118` Server IP address (Tailscale Interface)

## SRT Relay

### Relay Server
```bash
srt-live-transmit -v -srctime:yes "srt://0.0.0.0:5000?mode=listener&latency=2000" "srt://0.0.0.0:6000?mode=listener&latency=2000"
```

### Transmitter
```bash
ffmpeg -re \\
-f lavfi \\
-i testsrc=d=65585:s=1920x1080:r=23.97,format=yuv420p \\
-f lavfi -i sine=f=440:b=4 \\
-shortest \\
-mpegts_flags resend_headers \\
-muxrate 10M \\
-max_interleave_delta 0 \\
-f mpegts \\
"udp://127.0.0.1:5100?pkt_size=1316"
```

```bash
srt-live-transmit -srctime:yes \\
"udp://127.0.0.1:5100" \\
"srt://10.1.20.65:5000?mode=caller&latency=2000"
```

### Receiver
```bash
srt-live-transmit -srctime:yes \\
"srt://10.1.10.65:6000?mode=caller&latency=2000" \\
"udp://127.0.0.1:7000"
```