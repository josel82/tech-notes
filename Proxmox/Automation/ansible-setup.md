# ansible-setup
#ansible #Proxmox 

[source](https://www.youtube.com/watch?v=4G9d5COhOvI)
## Initial configuration
Install `sshpass` ont the management node. This will help us with the login process when connecting with the proxmox node. 
```bash
sudo apt install sshpass -y
```

Create an `inventory` file:
```yaml
[pvenodes]
192.168.100.10
192.168.100.11
192.168.100.12
```
This will provide ansible with the ip addresses of the proxmox servers.

Create an `ansible.cfg` file, and paste the following lines. This lines of configuration will override some of the default settings. This step is done to avoid some warnings.
```yaml
[default]
interpreter_python=auto_silent
host_key_checking=False
```

## Test connection
Run ansible as follows:
```bash
ansible pvenodes -i inventory -m ping --user=root -k
```

## Ansible Playbook
In the next step, will create a user account on the proxmox servers, to use with ansible, and we will use ansible to set this up. Lets create a playbook, and paste the following instructions:

`pve_onboard.yml`
```yaml
- hosts: pvenodes
  tasks:

  - name: install sudo package
    apt:
      name: sudo
      update_cache: yes
      cache_valid_time: 3600
      state: latest

  - name: create ansible user
    user:
      name: ansible
      shell: '/bin/bash'

  - name: add ansible ssh key
    authorized_key:
      user: ansible
      key: "<paste-ssh-public-key-here>"

  - name: add ansible to sudoers
    copy:
      src: sudoer_ansible
      dest: /etc/sudoers.d/ansible
      owner: root
      group: root
      mode: 0440
```

Make sure you create the file that we are referencing in the playbook, on the management device.

`~/files/sudoer_ansible`
```
ansible ALL=(ALL) NOPASSWD: ALL
```

Run the playbook:
```bash
ansible-playbook pve_onboard.yml -i inventory --user=root -k
```

Once we have successfully ran the previous command, we should be able to log in to the proxmox servers with the new user.

```bash
ansible pvenodes -m ping -i inventory --user=ansible --private-key ~/.ssh/ansible-key
```

## Ansible Proxmox API

To be able to access Proxmox API via Ansible, we need to do the following:

- Go to Proxmox Web interface and create a new user under the Linux PAM real  (Datacenter > Permissions > Users > Add)
- Give this user administrator permissions 
- Create an API token for this user. Make sure that the option "privilege separation" is unchecked. Keep copy and paste the Token ID and secret in a safe place.

Back in the management device, create a new playbook:
pve_install_proxmoxer.yaml
```yaml
- hosts: pvenodes
  become: true
  tasks:

  - name: update repository cache
    apt:
      update_cache: yes
      cache_valid_time: 3600
      
  - name: install promoxer
    apt:
      name: 
      - python3-proxmoxer
      state: latest

```

This playbook will install a piece of software in the PVE nodes which is necessary for Ansible to work with Proxmox API

Finally, run the playbook:
```bash
ansible-playbook pve_install_proxmoxer.yaml -i inventory --user=ansible --private-key ~/.ssh/ansible-key
```

### Test API
To test if Ansible is able to sucessfully access Proxmox API, we will try to crate a Virtual Machine using Ansible. Create the following playbook: 

pve_create_vm.yaml
```yaml
- hosts: 192.168.100.10
  become: false
  gather_facts: false
  tasks:

  - name: create new vm with minimal options
    vars: 
      ansible_python_interpreter: /usr/bin/python3
    proxmox_kvm:
      api_user: ansible@pam
      api_token_id: <TOKEN-ID-HERE>
      api_token_secret: <TOKEN-HERE>
      api_host: 192.168.100.10
      node: pve1
      name: vmtest
```

Run the playbook:
```bash
ansible-playbook pve_create_vm.yaml -i inventory --user=ansible --private-key ~/.ssh/ansible-key
```

### Problem
I encounter a problem trying to run the playbook above:

```
TASK [create new vm with minimal options] **************************************
fatal: [10.1.10.10]: FAILED! => {"changed": false, "msg": "Using \"token_name\" and \"token_value\" require proxmoxer>=1.1.0"}

```

Solution:
I manually upgraded the `proxmoxer` package to the latest version on each node:
```
pip3 install proxmoxer -U
```
