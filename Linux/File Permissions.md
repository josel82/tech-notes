# File Permissions
#Linux #Files #File_System 

`d rwx rwx rwx`

| Type | User | Group | Others |
|---|---|---|---|
| d | rwx | rwx | rwx |
| <p>d= directory</p> <p>-= file</p> | <p>r=read</p> <p>w=write</p> <p>x=execute</p> | <p>r=read</p> <p>w=write</p> <p>x=execute</p> | <p>r=read</p> <p>w=write</p> <p>x=execute</p> |

E.g.
```
-rw-r--r--   1 josel82  staff     0B  8 Aug 22:23 myFile.txt
```
On this output we can read that this is a "File", that its owner can "Read" and make changes ("Write") to it but can't execute it, and that members of the same group or other users can only read it.


## Adding permissions

Making a file executable
```bash
chmod +x myfile.txt
```

Only the owner can execute
```bash
chmod u+x myfile.txt
```

## Removing permissions

Remove execute permission to everyone
```bash
chmod -x myfile.txt
```

Prevent other users (that don't belong to your group) to execute this file
```bash
chmod o-x myfile.txt
```

Similarly you can change permissions for directories, but in that case read, write and execute permissions have a slightly different meaning:

r: permission to see the contents of the directory
w: permission to change the contents of the directory
x: permission to enter into the directory


## Setting Permissions with  numerical values

`chmod` command followed by a three digit number. Each digit is the sum of the values of `rwx` 

| Permission | On | Off |
|---|---|---|
| r | 4 | 0 |
| w | 2 | 0 |
| x | 1 | 0 |

| First digit | Second digit | Third digit |
|---|---|---|
| user | group | others |

- Example 1
```bash
chmod 400 textFile.txt
```
This command will produce the following permissions: -r--------

- Example 2
```bash
chmod 600 textFile.txt
```
This one will produce: -rw-------

- Example 3
```bash
chmod 700 textFile.txt
```
This will produce the following permissions: -rwx------

- Example 4
```bash
chmod 644 textFile.txt
```
Will produce the following permissions: -rw-r--r--