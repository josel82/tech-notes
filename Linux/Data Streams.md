# Data Streams
#Linux

In linux processes have 3 channels

**STDIN  -->  0**

**STDOUT --> 1**

**STDERR --> 2**

-   Standard In = takes input from somewhere <shell; file; web, etc>
-   Standard Out = it gives output directly on the shell, as a file, to the web, etc
-   Standard Error= different type of output (Error output)

## Redirect STDOUT
```bash
echo "Hello World"  1>  message.txt
```
or
```bash
echo "Hello World"  >  message.txt
```

### Append to a file
```bash
echo "My name is: Slim Shady" >> message.txt
```

## Redirect STDERR 
```bash
echo "this will produce an error" 2> errorLog.txt
```

## Redirect STDIN
```bash
mail -s "Important Message" josel82 < message.txt
```

## Print the first 10 lines of file
^910172
```bash
head /var/log/syslog
```

## Print the last 10 lines of file
```bash
tail /var/log/syslog
```

## Print the last 50 lines of file
```bash
tail  -n 50 /var/log/syslog
```

## Print the last 10 lines of file in follow mode
```bash
tail  -f /var/log/syslog
```
The prompt will flash and the output will update as new logs are shown.

## Pipes "|"

It allows to redirect the output of a command to the input of another command

```bash
ps -aux | less
```

Example
```bash
cat /var/log/syslog | grep apache2
```
Here the `grep` command takes in the STOUT of the `cat` command and filters it, printing only lines containing the string `apache2`