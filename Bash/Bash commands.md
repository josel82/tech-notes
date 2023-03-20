# Bash commands
#Bash 

#### Get the exit status of the last executed command
```bash
$?
```

#### Test command
This command checks if a expression is true or false. It returns 0 if the exprecion is true or 1 if the expresion is false
e.g.

```bash
test 5 = 4 && echo "True" || echo "False"
```
Output: False

```bash
test 5 = 5 && echo "True" || echo "False"
```
Output: True

```bash
[ "John" -ne "Phil" ] && echo $? || echo $?  
```
Output: 0

`[ expression ]` is another way to write `test expression`

##### Comparison operators
| Operator | Description | Operator|
|---|---|---|
| -lt | Less than | < |
| -gt | Greater than | > |
| -le | less or equal than | <= |
| -ge | greater or equal than | >= |
| -eq | equal | == |
| -ne | not equal | != |
| Work with [ ] and \[[ ]] | | Work only with \[[ ]] |   

##### String operators
| Operator | Description |
|---|---|
| -n | returns 0 if string is not empty or 1 if empty |
| -z | returns 0 if string is empty or 1 if not empty |

##### File directory operators
| Operator | Function |
|---|---|
| -e | File/directory exists |
| -f | is a file |
| -G | file exists and is owned by effective group ID |
| -d | is a directory |
| -s | file size greater than 0 |
| -L | is a symbolic link |
| -O | file exists and is owned by effective user ID |
| -S | is a socket |
| -r | file is readable |
| -w | file is writable |
| -x | file is executable |

##### Boolean operators
| Operator | Function |
|---|---|
| && | AND |
| \|\| | OR |
| ! | NOT |



