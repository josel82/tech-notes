# SRT Labs

## SRT Relay

### Relay Server

Host: ubuntu-streamer

```bash
srt-live-transmit -v -srctime:yes \\
"srt://0.0.0.0:5000?mode=listener&latency=2000" \\
"srt://0.0.0.0:6000?mode=listener&latency=2000"
```

### Transmitter

Host: pop-desktop

```bash
srt-live-transmit -srctime:yes \\
"udp://@239.1.1.10:5100" \\
"srt://10.1.20.65:5000?mode=caller&latency=2000"
```

### Receiver

Host: Macbook

```bash
srt-live-transmit -srctime:yes \\
"srt://10.1.10.65:6000?mode=caller&latency=2000" \\
"udp://127.0.0.1:7000"
```

VLC

`udp://@127.0.0.1:7000`

```bash
srt-live-transmit -v -srctime:yes \\
"srt://0.0.0.0:5000?mode=listener&latency=2000" \\
"srt://0.0.0.0:5022?mode=listener&latency=2000"
```