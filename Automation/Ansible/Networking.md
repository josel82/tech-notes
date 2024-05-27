# Networking
#Ansible #Networking 



## ansible.cnf
add or uncomment the following line:
```
host_key_checking=False
```
This is just so we don't need to upload ssh keys, assuming we are using this controller for training purposes and no for production.

## hosts
```
[switches]
sw1.ciscolab.home.arp
sw2.ciscolab.home.arp

[switches:vars]
ansible_user=admin
ansible_password=cisco
ansible_connection=network_cli
ansible_network_os=ios
ansible_port=8181 (Only if ports are differnet from default 22)
```

## Adhoc commands examples
```bash
ansible switches -m ping
```

```
ansible switches -m ios_command -a "commands='show ip int brief'" 
```

## Playbook example
`devnet.yml`
```yaml
---
- name: General Config
  hosts: switches
  tasks:
     - name: Add Banner
       ios_banner:
       banner: login
       text: | 
         Make couscous Algerian again
       state: present
    - name: Add loopback
      ios_interface:
         name: Loopback21
         state: present
 
```

```bash
ansible-playbook devnet.yml
```

In the case you want to undo the previous changes, just edit the `devnet.yml` file and change the value of the state variable to "absent", and run the playbook again.
```yaml
---
- name: General Config
  hosts: switches
  tasks:
    - name: Add Banner
      ios_banner:
         banner: login
         text: | 
            Make couscous Algerian again
         state: absent
    - name: Add loopback
      ios_interface:
         name: Loopback21
         state: absent
 
```

