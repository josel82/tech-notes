# SSH Server
#Linux #SSH 

## Preparation

Check if openssh is installed in your system. Run:

```bash
netstat -tupln
```
or
```bash
which sshd
```
or
```bash
systemctl status sshd
```

## Installation

If it's not installed you can do so with the following commands:

On Debian based distributions

```bash
sudo apt install openssh-server
```

On fedora

```bash
sudo dnf install openssh
```


Once installed, you should be able to connect remotely by running the following command from the SSH client:
```bash
ssh <username>@<ip address>
```
[[SSH Client]]

## Disable root login

1. Open the sshd_config file with your text editor of choice
```bash
sudo nano /etc/ssh/sshd_config
```
Change `PermitRootLogin yes` to `PermitRootLogin no`. Save changes and quit

2. Restart the ssh server
```bash
sudo systemctl restart ssh
```
Make sure you have a user account to log in to your server with before doing this, or else you will lock yourself out of the server.

## Disable Password Authentication

1. Open the sshd_config file. Uncomment and change `PasswordAuthentication yes` to `PasswordAuthentication no`. Save changes and quit

2. Restart the ssh server. Do this after you have set up key pair authentication before doing this or else you will lock yourself out of the server


#### Extra

If you want to check for failed attempts to log in your server:

```bash
sudo tail -n 50 /var/log/auth.log
```
