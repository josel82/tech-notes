# Package Management
#Linux 

## Fedora and CentOS

#### Yum

- Searching for packages
```bash
yum search <keyword>
```

- Installing a package
```bash
sudo yum install <package name>
```

- `y` option defaults all installation prompts to 'yes' (Use only in scripts)
```bash
sudo yum install  -y <package name>
```

- Removing a package
```bash
sudo yum remove  <package name>
```

- Updating package cache
```bash
sudo yum update
```

- Upgrading installed packages
```bash
sudo yum upgrade
```

#### dnf
`dnf` is the new package manage for fedora. But you can still use `yum` and it will redirect to `dnf` automatically.

```bash
sudo dnf upgrade
```


## Debian distros

#### Apt

- Searching for packages
```bash
apt search <keyword>
```

- Updating package cache
```bash
sudo apt update
```

- Upgrading installed packages
```bash
sudo apt upgrade
```

- `dist-upgrade` will install or remove a package if necessary.
```bash
sudo apt dist-upgrade
```

- Installing a package
```bash
sudo apt install <package name>
```

- Removing a package
```bash
sudo apt remove <package name>
```

- Removing package dependencies
```bash
sudo apt autoremove
```


