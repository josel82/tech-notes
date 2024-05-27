# Finding files
#BASH 

## Basic command
```bash
find /file/path -name "myFile.txt"
```

## Examples

- find any file in the, current working directory, which name ends in ".txt"
```bash
find . -name "*.txt"
```
- find an txt file in the, current working directory, which contains a specified piece of text
```bash
find . -name "*.txt" -exec grep -l "file contains this exact line of text" {} +
```
In this example, the `{}` is a place holder the `-exec` command uses to pass the output of the `find` command to the `grep` command. And the `+` concatenates all of the results of the `find` command, pass it to the `grep` command, running `grep` only once.

You can also end the `-exec` statement with `/;`
e.g.
```bash
find . -type f -exec echo {} /;
```
In this case, `-exec` will run `echo` for each result of the `find` command. `-type f` instructs to only search for "files" (and ignore directories).
