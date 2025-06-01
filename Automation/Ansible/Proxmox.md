
Credits to: [[Tech Tutorials - David McKone](https://www.youtube.com/@TechTutorialsDavidMcKone)](https://www.youtube.com/watch?v=4G9d5COhOvI&t=50s)

In the workstation
- Latest version of ansible
- `sshpass` package must be installed `sudo apt-get install sshpass -y`

Navigate to your working directory and create the following files

`inventory`
```
[pvenodes]
10.0.0.1
10.0.0.2
10.0.0.3
```

`ansible.cfg`
```
[defaults]
interpreter_python=auto_silent
host_key_checking=False
```

You can verify that Ansible can access the nodes using the following command:
```bash
ansible pvenodes -i inventory -m ping  --user=root -k 
```

Next we want to create a new user within proxmox, which ansible can use to connect with the servers. We are going to do this with an ansible playbook.

`pve_onboard.yml`
```yml
---
- hosts: pvenodes
  tasks:

  - name: install sudo package
    apt:
      name: sudo
      update_cache: yes
      cache_valid_time: 3600
      state: latest

  - name: create Ansible user
    user:
      name: ansible
      shell: '/bin/bash'

  - name: add Ansible ssh key
    authorized_key:
      user: ansible
      key: "public key here"
      #Create an SSH key without password for ansible

   - name: add ansible to sudoers
     copy:
      src: sudoer_ansible
      dest: /etc/sudoers.d/ansible
      owner: root
      group: root
      mode: 0440
```

Create the `sudoer_ansible` file you are referencing in the playbook, and paste the following:
`sudoer_ansible`
```
ansible ALL=(ALL) NOPASSWD: ALL
```

Inside the working directory, run the following command:
```bash
ansible-playbook pve_onboard.yml -i inventory --user=root -k
```

This playbook will create a new user within proxmox nodes and will copy an ssh public key. To verify ansible can connect with those credentials, run the following command:

```bash
ansible pvenodes -m ping -i inventory --user=ansible --private-key=~/.ssh/ssh-key
```

## Enable Proxmox API. 

We will start by creating a user. Open up Proxmox GUI and under `Datacenter/Permissions/Users` click on `add` and create the new user within the PAM realm.
Then go to `Datacenter/Permissions` click on `add` then give this user root permissions. 
Next, go to `Datacenter/Permissions/API tokens`, click on `add` and create a new token for this user.

We will also new to install an additional package within proxmox nodes, and we will use a playbook to do it.

`pve_install_proxmoxer`
```yml
---
- hosts: pvenodes
  become: true
  tasks:

  - name: update repository cache
    apt:
      update_cache: yes
      cache_valid_time: 3600

  - name: install proxmoxer
    apt:
      name:
      - python3-proxmoxer
      state: latest
```

Run the following command:
```bash
ansible-playbook pve_install_proxmoxer.yml -i inventory --user=ansible --private-key=~/.ssh/ssh-key
```

Now we should be able to use Proxmox API. We can verify this by running a simple playbook that create a VM in a specified PVE node.

`pve_create_vm.yml`
```yml
---
- hosts: 192.168.10.10
  become: false
  gather_facts: false
  tasks:

  - name: Create new vm with minimal options
    vars:
      ansible_python_interpreter: /usr/bin/python3
    proxmox_kvm:
      api_user: ansible@pam
      api_token_id: ansible-token
      api_token_secret: insert-token-here
      api_host: 192.168.10.10
      node: pve-node1
      name: vm-test
```

We then run the playbook:
```bash
ansible-playbook pve_create_vm.yml -i inventory --user=ansible --private-key=~/.ssh/ssh-key 
```

We can then delete that VM with the following playbook:

`pve_remove_vm.yml`
```yml
---
- hosts: 192.168.10.10
  become: false
  gather_facts: false
  tasks:

  - name: Remove example VM
    vars:
      ansible_python_interpreter: /usr/bin/python3
    proxmox_kvm:
      api_user: ansible@pam
      api_token_id: ansible-token
      api_token_secret: insert-token-here
      api_host: 192.168.10.10
      node: pve-node1
      name: vm-test
      state: absent
```


```bash
ansible-playbook pve_remove_vm.yml -i inventory --user=ansible --private-key=~/.ssh/ssh-key 
```