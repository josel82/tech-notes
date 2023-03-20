# Solutions to common issues
#Linux #Issues #Solutions #SSH

Problem:
```
no matching host key type found. Their offer: rsa-sha2-512,rsa-sha2-256,ecdsa-sha2-nistp256,ssh-ed25519
```

Solution:
[https://www.analysisman.com/2018/08/linux-ssh.html](https://www.analysisman.com/2018/08/linux-ssh.html)

Problem:
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@   @ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! @   @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@   IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!   Someone could be eavesdropping on you right now (man-in-the-middle attack)!   It is also possible that a host key has just been changed.   The fingerprint for the ECDSA key sent by the remote host is   SHA256:UX/eJ3HZT9q6lzAN8mxf+KKAo2wmCVWblzXwY8qxqZY.   Please contact your system administrator.   Add correct host key in /home/sk/.ssh/known_hosts to get rid of this message.   Offending ECDSA key in /home/sk/.ssh/known_hosts:4   ECDSA host key for 192.168.1.102 has changed and you have requested strict checking.   Host key verification failed.
```

```bash
ssh-keygen -R <remote-system-ip-address>
```

Solution:
[https://ostechnix.com/fix-ecdsa-host-key-warning-error-arch-linux/](https://ostechnix.com/fix-ecdsa-host-key-warning-error-arch-linux/)