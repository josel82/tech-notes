# HDD Health Check
#Linux #Storage 

For this you'll need the `smartmontools` package installed on your system. If you don't have it, install it as follows:
```bash
sudo apt install smartmontool
```

then run:

```bash
sudo smartctl --all /dev/name_of_device
```

e.g:

```bash
sudo smartctl --all /dev/sdb
```
