# Secure Copy
#Linux #Files #Security

[Documentation](https://www.ionos.com/digitalguide/server/configuration/linux-scp-command/)

```bash
scp /local/file/path username@server_ip:/remote/path
```
If you don't include the remote path, scp will copy the file in the home folder at the remote server.

## Using SSH key
```bash
scp -i /path/to/ssh/key /path/to/file username@server_ip:/path/to/directory
```

## Copying a directory

```bash
scp -r myLocalDir/  username@172.115.50.10:/home/myRemoteDir/
```

## Reverse Copy

```bash
scp username@172.115.50.10:/home/username/myFile .
```