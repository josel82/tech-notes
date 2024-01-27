# Solutions to common issues
#Linux #Issues #Solutions #SSH



Problem:
```
no matching host key type found. Their offer: rsa-sha2-512,rsa-sha2-256,ecdsa-sha2-nistp256,ssh-ed25519
```


[Solution:](https://www.analysisman.com/2018/08/linux-ssh.html)
Open up the terminal. We will be editing the `/etc/ssh/ssh_config` file, but before you do, create a backup of the current version of the file. You might need to use `sudo` to run this commands:
```bash
sudo cp /etc/ssh/ssh_config /etc/ssh/ssh_config.bak
```

Now, open the file with the text editor of your choice, I will use nano:
```bash
sudo nano /etc/ssh/ssh_config
```

Uncomment these two lines (remove the `#` signs):
```bash
# MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160  
# Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc
```

Finally add these two lines at the bottom of the file:
```bash
HostkeyAlgorithms ssh-dss,ssh-rsa,ssh-ed25519,rsa-sha2-512,rsa-sha2-256  
KexAlgorithms +diffie-hellman-group1-sha1
```


Problem:
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@   @ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! @   @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@   IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!   Someone could be eavesdropping on you right now (man-in-the-middle attack)!   It is also possible that a host key has just been changed.   The fingerprint for the ECDSA key sent by the remote host is   SHA256:UX/eJ3HZT9q6lzAN8mxf+KKAo2wmCVWblzXwY8qxqZY.   Please contact your system administrator.   Add correct host key in /home/sk/.ssh/known_hosts to get rid of this message.   Offending ECDSA key in /home/sk/.ssh/known_hosts:4   ECDSA host key for 192.168.1.102 has changed and you have requested strict checking.   Host key verification failed.
```

This issue occurs when the remote server, for some reason, has regenerated its ssh keys. When the client compares the new public key with the one in the `~/.ssh/known_hosts` file, it detects there has been a change and produces this warning. 

[Solution](https://ostechnix.com/fix-ecdsa-host-key-warning-error-arch-linux/)

If we are aware of a change of ssh key on the server (We may have done the change ourselves or an authorized administrator), then we can proceed by running the following command:

```bash
ssh-keygen -R <remote-system-ip-address>
```

What this command does is, it removes the previous ssh key from the `known_hosts` file.

