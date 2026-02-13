# Working with branches
#Git #Commands 

## Listing branches
```bash
git branch
```

## Create a new branch
This command will create anew branch based on the currently checked out revision
```bash
git branch my-new-branch
```
Create a new branch on a specific revision
```bash
git branch other-branch <revision-hash>
```

## Switch branch
```bash
git checkout my-new-branch
```
Newer command specifically for switching branches
```bash
git switch other-branch
```
Switching to the main branch
```bash
git switch main
```

## Rename branches
This will rename the currently active branch
```bash
git branch -m better-branch
```
You can change the name of a non-head branch with:
```bash
git branch -m my-new-branch my-better-branch
```

## Publishing branches
```bash
git push -u origin <local-branch>
```
the `-u` flag establishes a tracking connection between the remote and the local branch

## Tracking branches
The following pulls a remote branch that is not present in the local repository while establishing  a tracking connection.
```bash
git branch --track feature/login origin/feature/login
```
or
```bash
git checkout --track origin/feature/login
```
since we didn't pass a name for the 'local' branch the `git checkout` command will give the local branch the name of the remote branch by default

## Pulling and pushing branches
Once we have stablished a tracking connection as in the examples above, we can then use the following commands and git will know which branch you are pulling from or pushing to
```bash
git pull
```

```bash
git push
```

The following gives you a status of the divergence between the local and the remote branch
```bash
git branch -v
```


## Deleting branches
Delete a local branch
```bash
git branch -d feature/login
```
Note: you cannot delete the Head (currently active) branch. If you want to delete the branch you are currently on, you need to first switch to another branch.

Delete and remote branch
```bash
git push origin --delete feature/downloader
```

## Merging branches
Integrating changes from another branch into your local HEAD branch

1. Make active the branch that should receive the changes
```bash
git switch main
```
2. Execute the the `merge` command with the name of the branch that contains the changes
```bash
git merge feature/uploader
```