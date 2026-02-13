# Getting Started
#Git 

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


## Ignoring files in the repository's directory
Inside the repository's directory, create a file `.gitignore`. Inside this file write the name of the files you want to be ignored. Here is an example:
```
# Ignore all .txt files
*.txt
```
In this example we have told Git to ignore any .txt inside the repository's directory.
[Documentation](https://github.com/github/gitignore)