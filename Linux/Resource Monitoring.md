# Resource Monitoring
#Linux #Resources

## Memory info

```bash
free
```

```bash
free -m
```


## Swap

Swap is HDD space that the Linux Kernel allocates for processing data once the memory is full. When installing a Linux distro, the Linux Kernel creates a Swap partition for this purpose. Generally the installation wizard asks the user what size they want their Swap partition to be. The recommended sizes are:

If your memory = 1Gb RAM                         => Swap should be twice (2Gb)

If your memory is between 2Gb and 4Gb => Swap should be half your memory

If your memory is more than 4Gb                => Swap should be 2Gb


## Disk space

- Displays free disk space.
```bash
df
```

- "Human-readable" output.  Use unit suffixes: Byte, Kilobyte, Megabyte, Gigabyte, Terabyte and Petabyte in order to reduce the number of digits to three or less using base 2 for sizes.
```bash
df -h
```

- Include statistics on the number of free inodes.
```bash
df -i
```


## CPU, Memory usage and Load average

```bash
top
```
or
```bash
htop
```


## Load average

```bash
uptime
```

