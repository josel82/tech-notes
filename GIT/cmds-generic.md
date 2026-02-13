# Generic commands
#Git #Commands 

## Check the status of a repository
```bash
git status
```
shorter output version
```bash
git status -s
```

## List the files in the staging area
```bash
git ls-files
```


## Adding files to the staging area

Add a file to the staging area
```bash
git add my_file
```
add multiple files
```bash
git add my_file1 my_file2
```
add all files in the working directory
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


## Committing files
```bash
git commit -m "commit description"
```
or
```bash
git commit 
```
to write a longer description for the commit on the default editor

commit skipping the staging face
```bash
git commit -a -m "latest update"
```


## Comparing changes
Compares what we have in the working directory with what there is in the stage area
```bash
git diff
```
Run the following to see the staged changes that are going in the next commit 
```bash
git diff --staged
```
Using diff tool. Refer to [[configuration#Set VSCode a the diff tool]] 
```bash
git difftool
```
or
```bash
git difftool --staged
```


## Moving files back to the "Working files" environment
```bash
git restore --staged <file>
```   
[[concepts#Git Environments]]


## Removing files
Files can be removed in two ways
1. Remove the file from the working directory, then "add" the change to the staging area.

2. Using the `rm` command.  The `rm` command skips the staging step.

This will remove a file from both the working directory and staging area.
```bash
git rm "myFile.html"
```
The following will only remove the file from the staging area 
```bash
git rm --cached "myFile.html"
```
The next command will remove a directory from the staging area
```bash
git rm --cached -r my_folder/
```


## Undo changes previously added to the staging area
```bash
git restore --staged file1.js
```
multiple files
```bash
git restore --staged file1.js file2.js
```
pattern
```bash
git restore --staged "*.js"
```
everything
```bash
git restore --staged .
```


## Discarding local changes 
Undo changes in the working directory. This changes haven't yet been added to the staging area
```bash
git restore file1.js
```
all local changes
```bash
git restore .
```
These command only undo changes on tracked files

If you want to remove untracked files
```bash
git clean -fd
```
flags: (f) force (d) directories


## Restoring a file from the previous version
The following restore `file1.js` to the version before the last commit
```bash
git restore --source=HEAD~1 file1.js
```


## Read the commit history
```bash
git log
```
Short summary
```bash
git log --oneline
```
In reverse order
```bash
git log --oneline --reverse
```
for more detailed information
```bash
git log -p
```


## Viewing a commit
```bash
git show <commit-id>
```
last commit
```bash
git show HEAD
```
x steps back from the HEAD pointer
```bash
git show HEAD~2
```
you want to see a specific file in a particular commit
```bash
git show HEAD~2:app/myfile
```
list all files in a commit
```bash
git ls-tree HEAD~1
```


## Amend the previous commit
```bash
git commit -m "Amended commit message" --ammed
```
This will amend the commit on top of the heap


## Going back to an earlier commit
1. Run the following command and identify the commit you want to go back to and grab its hash number. 
```bash
git log --oneline
``` 

2. Now run: 
```bash
git reset <hash#>
```


## Modifying the commit history
```bash
git rebase -i --root
```
This will bring you to an editor where you are able to modify how things appear in the history.


## Renaming files
This can be done in two ways:
1. The long way
	- Rename the file in the working directory
	- Add the change to the staging area
	- Add the renamed file to the staging area
```bash
git add old_file_name
```

```bash
git add new_file_name
```

2. The shorter way
```bash
git mv old_file_name new_file_name
```


