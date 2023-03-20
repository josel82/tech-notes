# Aliases
#Bash 

We can use an alias to abreviate long commands that we use often, so that we don't have to type the long command every single time.

## Creating an alias

```bash
alias ls='ls -als'
```
from this point on, every time we run the 'ls' command, the system would be running 'ls -als' instead.

Other examples:
 - Weather forecast tool
```bash
alias wtr='curl wttr.in'
```

-  speed test tool
```bash
alias speedtest='curl -s https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py | python3 -'
```

## Make Aliases permanent

Creating aliases as shown above works, but it only does for that terminal session. If you open another session, your aliases won't be there.

If you want to make your aliases permanent you have to add them in your `.bashrc` file. Open your `.bashrc` file with your favorite text editor:
```bash
nano ~/.bashrc
```

go to the end of the file and add your aliases:
```bash
# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
if ! shopt -oq posix; then
  if [ -f /usr/share/bash-completion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
  elif [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
  fi
fi

# My Aliases
alias speedtest='curl -s https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py | python3 -'

alias wtr='curl wttr.in'
```
