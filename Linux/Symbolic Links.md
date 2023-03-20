# Symbolic Links
#Linux #File_System

Files that point to another file. Very similar to a desktop shortcut in Windows.

```bash
ls -l /etc/
``` 
![resolv.conf.png](../Images/resolv.conf.png)

Symbolic links are represented with an arrow that point to the path of the file they are linked to.

Here is how you create a symolic link:
```bash
ln -s /home/josel82/Documents/Weekly_Report.txt /home/josel82/Desktop/
```



