# SSH Client
#Linux #SSH 

## Connection

1. Using password authentication:
```bash
ssh <username>@<ip_address>
```

2. Using SSH key pair
```bash
ssh -i <private_key_path> <username>@<ip_address>
```


## Config file
This file lives in `~/.shh/` directory. Inside this file, we can register details of different remote servers which we can reference in the ssh command with the `Host` variable.

```bash
sudo nano ~/.ssh/config
```

```config
Host myServer
	HostName 192.168.0.100
	User admin


Host raspPi
	HostName 192.168.0.55
	User piAdmin
	IdentityFile ~/.ssh/pi_key

```

We can reference the remote hosts in the example above as follows:

```bash
ssh myServer
```

```bash
ssh rasPi
```
