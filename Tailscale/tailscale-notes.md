
# Tailscale notes

## Adding a subnet router node to your Tailscale network
```bash
## For a Debian Bookworm host
#############################
curl -fsSL <https://pkgs.tailscale.com/stable/debian/bookworm.noarmor.gpg> | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL <https://pkgs.tailscale.com/stable/debian/bookworm.tailscale-keyring.list> | sudo tee /etc/apt/sources.list.d/tailscale.list
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install tailscale

## Enables IP forwarding
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
sudo sysctl -p /etc/sysctl.d/99-tailscale.conf

## Start Tailscale
sudo tailscale up --auth-key=<token-here>?ephemeral=false --advertise-tags=tag:home-network --ssh --advertise-routes=172.16.27.0/24

```

## Adding a Linux server

1. Create a new tag

Go to `Access controls` and edit the configuration file

```bash
"tagOwners": {
		"tag:servers":        ["group:admin"],
	},
```

1. Create an OAuth token

`Settings -> Trust Credentials -> + Credential`

	1.1 Select `OAuth`, add a description and click on “Continue”

`Devices → Core → Read and Write`

	1.2 add the tag you created previously

`Keys -> Auth Keys -> Read and Write`

	1.3. add the tag you created previously

	1.4. generate the token and save it on a safe place

2. On the server

```bash
sudo tailscale up --auth-key=<token-here>?ephemeral=false --advertise-tags=tag:server --ssh

```

3. Set the appropriate permissions in the Access Controls configuration

```bash
"acls": [
		{
			"action": "accept",
			"src":    ["tag:management"],
			"dst": [
				"tag:servers:*",
			],
		},
```

## Reseting Tailscale in Linux

```bash
sudo tailscale down
sudo tailscale up --advertise-tags "tag:management" --accept-routes
```