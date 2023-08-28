# PATH env variable
#Linux #Commands #Config

`$PATH` is an environment variable that contains the paths of directories that contain all the commands we run, such as `ls`, `cp`, `mv`, `find`, etc... otherwise we would need to write the full path of the file if I wanted to execute a script. E.g. `/usr/bin/ls` 

We are able to run `ls` from any directory because the path of the directory that contains this script is in the `$PATH` variable.

Lets have a look at the default value of `$PATH` in ubuntu 22.10
```bash
cat $PATH
```
```
cat: '/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin': No such file or directory
```

If I created a script `hello`
```bash
#!/bin/bash

echo Hello World

```

and I try to run it, I would optain:
```bash
hello
```
```
hello: command not found
```

If I wanted to run this script I would have to do it as follows
1. make the file executable `chmod +x hello`
2. then run it like so:
```bash
./hello
```
which literally specifies the paht of the file, the '.' meaning 'current irectory'

Now, if I wanted to run this script as a command I have a couple of options:
1. I could move the file to one of the paths in the `$PATH` variable. 
E.g. 
```bash
mv hello /usr/local/bin/
```

2. or I could add a new directory to the `$PATH` variable. E.g.
```bash
mkdir ~/bin
mv hello bin/
PATH=$PATH:~/bin  
```

## IMPORTANT!
Adding a path to the `$PATH` variable will only last for the duration of the current session. Whenever you open a new session the `$PATH` variable will default back to its original value.
If you want this change to stick you will need to add the following script to your `.bashrc` file:

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

# End of the file

if [ -d ~/bin ]; #here we check if the ~/bin directory exists
then
	PATH=$PATH:~/bin
fi

```

done this way we make sure that if for any reason the `~/bin` doesn't exist, the terminal doesn't throw errors