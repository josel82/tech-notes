# Useful commands
#Git #Commands 

- Cheking the status of a repository
```bash
git status
```

- Adding files to a repository: 
```bash
git add <file>
```

- Removing a file from a repository
```bash
git rm <file>
```

- Ignoring files in the repository's directory
Inside the repository's directory, create a file `.gitignore`. Inside this file write the name of the files you want to be ignored. Here is an example:
```
# Ignore all .txt files
*.txt
```
In this example we have told Git to ignore any .txt inside the repository's directory.
[Documentation](https://github.com/github/gitignore)

- Adding all the files
```bash
git add --all
```
or
```bash
git add -A
```
or
```bash
git add .
```

- Commiting files
```bash
git commit -m "First commit"
```

- Checking for modifications
```bash
git diff
```

- Movinging files back to the "Working files" environment
```bash
git restore --staged <file>
```   
[[GIT/Concepts#Git Environments]]

- Commiting files skipping the Stagging face
```bash
git commit -a -m "latest update"
```

- Deleting a file
```bash
git rm "myFile.htm"
```

- Restoring deleted file
```bash
git restore "myfile.htm"
```

- Changing a file's name
```bash
git mv "old name.txt" "new name.txt"
```

- Commit history
```bash
git log
```
or
```bash
git log --oneline
```
or
```bash
git log -p
```
for more detailed information

- Amend the previous commit
```bash
git commit -m "Amended commit message" --ammed
```
This will amend the commit on top of the heap

- Going back to an earlier commit
1. Run the follwing command and identify the commit you want to go back to and grab its hash number. 
```bash
git log --oneline
``` 

2. Now run: 
```bash
git reset <hash#>
```

- modifying the commit history
```bash
git rebase -i --root
```
This will bring you to an editor where you are able to modify how things appear in the history.

