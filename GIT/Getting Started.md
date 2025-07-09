# Getting Started
#Git 

## Initial configuration

1. From the home directory we start by setting the username:
```bash
git config --global user.name "Your name"
```

2. Next, we set email:
```bash
git config --global user.email your@email.com
```

3. Then we initialise the default branch:
```bash
git config --global init.default branch main
```

4. If we need some help with the configuration:
```bash
git config -h
```
or
```bash
git help config
```

## Create a repository
1. Go to the directory you want to create the repository into:
```bash
cd /Documents/Repos/myRepo1
```

3. Initialize the repository:
```bash
git init 
```

## Add changes to repository

```bash
git add file_path
```
add all changes
```bash
git add .
```

## Commit changes
```bash
git commit -m "Type a message describing the commited changes"
```

