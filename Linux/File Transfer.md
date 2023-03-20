# File Transfer
#Linux #Files #File_System 

## RSYNC
[rsync](https://en.wikipedia.org/wiki/Rsync) is a utility for efficiently transferring and synchronizing files between a computer and a storage drive and across networked computers by comparing the modification times and sizes of files.

- Copying local file to a remote disk.
```bash
rsync local-file user@remote-host:remote-file
```

- Copying local directory to a remote disk.
```bash
rsync -r /localDir <username>@<ip address>:/remoteDir
```

- Add the -v (verbose) option if you want to see output.
```bash
rsync -rv <local path> <username>@<ip address>:<remote path>
```

- This options will not only add the previous features but also others such as compression. For more info read the man page.
```bash
rsync -avz <local path> <username>@<ip address>:<remote path>
```


## SCP
[[Secure Copy]]
**scp** copies files between hosts on a network. It uses ssh for data transfer, and uses the same authentication and provides the same security as a login session.


``

``



``



