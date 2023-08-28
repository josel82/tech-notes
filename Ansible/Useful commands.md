# Useful commands
#Ansible 

Help
```bash
ansible --help
```

Ansible TUI (Terminal User Interface)
```bash
ansible-navigator
```

Run a playbook with `ansible-navigator` (Standard Mode)
```bash
ansible-navigator run myPlaybook.yml
```

Standard Out Mode. The output is similar to that you will get by running `ansible-playbook` command.
```bash
ansible-navigator run myPlaybook.yml --mode stdout
```

Check mode
```bash
ansible-navigator run myPlaybook.yml --mode stdout --check
```
In this mode, Ansible won't make any changes. Useful in cases when you want to test automation without applying any changes

Gathering facts
```
ansible -m setup localhost
```
in this example we gather facts of the local machine



