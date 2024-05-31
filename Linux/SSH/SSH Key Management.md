# SSH Key Management
#Linux #SSH 

Source: [Getting Started with OpenSSH Key Management](https://www.youtube.com/watch?v=GxRu35fy-oY&t=922s)


In Linux and Mac, SSH keys and configuration files live inside the `~/.ssh` directory

Basically, we will be generating an SSH key pair for each server we want to connect to and we are going to keep them inside the .ssh directory

For generating SSH keys we are going to use openSSH. Normally this will come preinstalled on most Linux distros and MacOS but you can check with the following command:

```bash
which ssh-keygen
```

Output: `/usr/bin/ssh-keygen`

If you don't get any output it means that openSSH is not installed in your host.

## Generating Keys | Standard Procedure

Now, to create a standard rsa key pair, run the following command:  (The 'C' options stands for "comment")

```bash
ssh-keygen -C "server1_key"
```

OpenSSH will prompt you for path and file name of the new key, while giving you default values. Be careful you don't override an existing by accepting the default values. It is better provide a different name for every new key pair

Provide the keys name by typing the full path e.g:

Generating public/private rsa key pair.

Enter file in which to save the key  (/home/username/.ssh/id_rsa): `/home/username/.ssh/server1_key
`
Press enter. Then provide a passphrase. This is optional, you can skip this by just pressing enter, but it is best practice to provide a passphrase for better security.

Enter passphrase (Empty for not passphrase):

Press enter and two files will be created: 'server1_key' and 'server1_key.pub' which are the private key and the public key respectively

## Generating Key | ed25519 Encryption Algorithm

There's a better way for creating SSH Keys: (The 't' options stands for "type")

```bash
ssh-keygen -t ed25519 -C "server2_key"
```

The rest of the process is the same as the one above. But in this case we generate a key pair with a better encryption algorithm.

The Next step will be copying the public key to the server we want to connect to:

```bash
ssh-copy-id -i ~/.ssh/server2_key.pub username@server_ip
```
The server will ask for a password for the connection (This is the user's password, not the key passphrase), press enter and the key should be copied successfully

This public key will be appended to `/home/username/.ssh/authorized_keys` file #Public_key

You can now connect to the server as follows:
```bash
ssh -i ~/.ssh/server2_key  username@server_ip
```

If we want this connection to be secured with the key instead of a password, open the 'sshd_config' file on the server side:
```bash
sudo nano /etc/ssh/sshd_config
```

And change: 'PasswordAuthentication yes' to 'PasswordAuthentication no'

Also uncomment: 'PubkeyAuthentication yes'

Save and close the file. Then restart the ssh service:

```bash
systemctl restart sshd.service
```

Next time you login via ssh you will be entering the passphrase instead of the user password. This will also prevent any user that doesn't have a key pair configured from connecting.
