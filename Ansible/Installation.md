# Installation
#Ansible #Linux 

## Requirements
### Control node requirements
- Any Unix-like Machine (including Windows Subsystem for Linux WSL distribution)
- Python ≥3.9

### Managed node requirements
- Python 2.7, 3.5-3.11
- User account that can SSH to the node with an interactive POSIX shell

## Locating Pyhton
```bash
python3 -m pip -V
```
If your current version of python3 is lower than the required, upgrade python3 to the correct version following the instructions on this link [[How to upgrade Python]]

In case you get  `No module name pip`  you will need to install `pip` under the selected version of Python.

```bash
sudo apt install python3-pip -y
```
[[How to install Python]]

## Installing Ansible with PIP
```bash
python3 -m pip install --user ansible
```

alternatively
```bash
python3 -m pip install --user ansible-core==2.12.3
```

check if Ansible was indeed installed
```
ansible --version
```

## Installing Ansible on CentosOS
```bash
yum update -y
```

```
yum install epel-release -y
```

```bash
yum install ansible -y
```

Config files should be located at `/etc/ansible`

## Installing Ansible on Ubuntu
```bash
sudo apt update
```

```bash
sudo apt install software-properties-common
```

```bash
sudo add-apt-repository --yes --update ppa:ansible/ansible
```

```bash
sudo apt install ansible
```

## Installing Ansible on other distributions

[# Installing Ansible on specific operating systems](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu)

