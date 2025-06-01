# Automating Scripts
#Linux #Scripts 

script.sh
```
#!/bin/bash


DATE=$(date '+%Y-%m-%d %H:%M:%S')

echo 'This script ran at $DATE'

```


## Crontab
Run the command with as root, so the script is ran by the root user, that way avoiding any permission errors.
```bash
sudo crontab -e
```

Select your preferred text editor, then append to the crontab file:
```
# m h  dom mon dow   command
30 3 * * * /home/myuser/script.sh
```
In this example the script will run every day at 03:30

If you want to verify crontab added the task, run the following command:
```bash
sudo crontab -l
```

