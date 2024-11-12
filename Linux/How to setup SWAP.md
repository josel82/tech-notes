Create a swap file:
```bash
sudo dd if=/dev/zero bs=1M count=5120 of=/mnt/5GiB.swap
```
in this example we are creating a 5GiB swap partition

Change permissions of the swap file:
```bash
sudo chmod 600 /mnt/5GiB.swap
```

Create swap partition:
```bash
sudo mkswap /mnt/5GiB.swap
```

Enable swap:
```bash
sudo swapon /mnt/5GiB.swap
```

Verify that the swap was created:
```bash
cat /proc/swaps
```

Add the swap to fstab. This will make sure the swap is mounted every time the VM boots up.
```bash
echo '/mnt/5GiB.swap swap swap defaults 0 0' | sudo tee -a /etc/fstab
```