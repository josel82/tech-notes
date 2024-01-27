# AddHoc commands


## A quick note before we start
When working with Ansible, there are two important files we need to be aware of. These are `/etc/ansibe/ansible.cfg` and `/etc/ansible/hosts`.

`ansible.cfg` is holds Ansible's configuration. We will need to edit this file if we want to change en default configuration, for any specific reson.

Then, we have the `hosts` file. And here is were we declare all of the devices we want to manage with Ansible, it is our inventory.

By default, these files are located in `/etc/ansible` directory, but we could create our own configuration file and inventory and place them in our working directory. When running Ansible commands, the config file in the working directory overrides the one in `/etc/ansible` directory. Then inside the local config file we can add the following line, under `[defaults`:
```
inventory = [filename]
```
This line will tell Ansible to use the local inventory file instead of the default `/etc/ansible/host` file.

## Pinging hosts
In this example we assume we have previously created SSH keys and copied them into the target servers [[SSH Key Management]]. Also that we are running this command from the same directory where the `inventory` file is in. 
```
ansible all --key-file ~/.ssh/mySSHKey -i inventory -m ping
```
Flags:
--key-file : SSH private key's file path
-i : inventory
-m : module (for this example we are using the `ping` module)

We could make this command shorter if we create a local `ansible.cfg` and add the following lines:

```
# ansible.cfg

[defaults]
inventory = inventory
private_key_file = ~/.ssh/mySSHKey
```

Then we can run the following command with the same results:
```
ansible all -m ping
```

## List all hosts

```
ansible all --list-hosts
```

## Obtain info about hosts

```
ansible all --gather-facts
```

targeted:
```
ansible all --gather-facts --limit [IP address]
```
