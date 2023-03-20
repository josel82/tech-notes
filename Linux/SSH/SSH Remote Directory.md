# SSH Remote Directory
#Linux #SSH #File_System #sshfs

Scenario
We want to mount a remote directory on our workstation. The next series of steps will walk you through on how to set this up.

## Preparation

1. Check if `sshfs` is available in your system. In Debian systems you can do so with:
```bash
apt search sshfs
```

In other Linux distros
```bash
yum search sshfs
```

In macOS
```zsh
brew search sshfs
```

If `sshfs` is not available in your system, you can install it by running:
```bash
sudo apt update
sudo apt install sshfs
```

2. Make sure you can connect to the remote server via SSH. [[SSH Client]]
```bash
ssh username@<server_IP_address>
```

3. On your work station, create a directory where you want to mount the remote directory
```bash
mkdir ~/remoteDir
```


## Mounting the remote directory

4. Mount the remote directory with `sshfs`. Run the following command on your workstation:
```bash
sshfs username@<server_IP_address>:/remote/directory/path /home/remoteDir
```

5. Check if the directory has been mounted correctly
```
mount
```
and see if the remote directory is listed


## Unmounting 

To unmount the remote directory, run the following command:
```
umount ~/remoteDir
```

or you can use the `sshfs` dedicate command for unmounting directories
```bash
fusermount -u ~/remoteDir
```