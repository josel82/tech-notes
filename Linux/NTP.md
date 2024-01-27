
# Public servers

## ntp.org
### Ireland servers
Stratum 1 - 2 servers
```
0.ie.pool.ntp.org
1.ie.pool.ntp.org
2.ie.pool.ntp.org
3.ie.pool.ntp.org
```

## Google
Stratum 1 servers
```
time1.google.com
time2.google.com
time3.google.com
time4.google.com
```

## Cloudflare
Stratum 3 server
```
time.cloudflare.com
```


## Docker container
[cturra/ntp](https://github.com/cturra/docker-ntp)

Pull from docker hub:
```
 docker pull cturra/ntp
```

Run the container:
```
docker run --name=ntp            \
           --restart=always      \
           --detach              \
           --publish=123:123/udp \
           cturra/ntp
```

Or run ntp with higher security
```
docker run --name=ntp                           \
           --restart=always                     \
           --detach                             \
           --publish=123:123/udp                \
           --read-only                          \
           --tmpfs=/etc/chrony:rw,mode=1750     \
           --tmpfs=/run/chrony:rw,mode=1750     \
           --tmpfs=/var/lib/chrony:rw,mode=1750 \
           cturra/ntp
```



# Clients

### Ubuntu systems
https://ubuntu.com/server/docs/use-timedatectl-and-timesyncd
Check current status of time
```
timedatectl status
```

Man pages:
```
man timedatectl
```

#### Time synchronisation
Check `timesyncd` status
```
systemctl status systemd-timesyncd
```

Configure `timesyncd` by editing the following file:
```
/etc/systemd/timesyncd.conf
```
The entries for `NTP=` and `FallbackNTP=` are space-separated lists. 


### ntpdate

`ntpdate` https://www.ntp.org/documentation/4.2.8-series/ntpdate/

#### Installation
- Debian based distros `apt-get install ntpdate`

#### Usage

Query server
```
ntpdate -q <ntp server IP>
```