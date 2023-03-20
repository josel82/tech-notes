# Finding files
#Linux #Files #File_System 

Name ending in "log"
```bash
find / -name *.log 2> /dev/null
```

Directory with name containing "log"
```bash
find /var -type d -name "*log*" 2> /dev/null
```

Directory with name containing "log" that has been modified in the last 7 days
```bash
find /var -type d -name "*log*" -mtime 7
```

### Flags 

- type d = only directories
- type f = only files
- mtime 7 = modified in the last 7 days

### Output redirection
```bash
2> /dev/null 
```
Discard errors 

### Regular expression
- `*.log` = ends with word
- `log*` = begins with word
- `*log*` = contains word
- `log` = exact word
