# User Management
#Linux #Users

- Create an user
```bash
sudo adduser ronaldoc
```
 
 - Create a group
```bash
sudo groupadd manutd
```

- Add user to a group
```bash
sudo usermod -aG manutd ronaldoc
```

- Change user login
```bash
udo usermod -l ronaldoc cristianor
```

-  Change user's password
```bash
sudo usermod -p new_password
```
**Security note:** you may want to add a space at the beginning of this command so it does't appear in the shell history.

-  Lock user out of server
```bash
sudo usermode -L cristianor
```

-  Unlock user
```bash
sudo usermod -U cristianor
```

-  Set expiration date to user account
```bash
sudo usermod -e 2022-08-08
```
Note that all this commands are run with the "sudo" command in front. This is because these command require root privileges.`

If you want to be able to manage user accounts you have two options. 
1. Login as root 
2. Give your user account permissions.`
You can give yourself permissions by adding your user to the "sudo" group. You will need to log in as root to do this:`

```bash
usermod -aG sudo myUser
```
Now  myUser will be able to run all commands just by placing "sudo" at the beginning. You can also modify the `sudoers` file (/etc/sudoers) but this is not recommended.

The following will place sudo before the previous command
```bash
sudo !!
```


## Configuration Files

`/etc/passwd`
This file contains a list of all users and info related to them

`/etc/sudoers`
Very important file which defines the powers of users and groups. Due to security reasons, it is best practice not to edit this file directly but instead run the following command:

- Best practice for editing the `sudoers` file. This command will open the `sudoers` file with vim text editor and it will validate the syntax upon saving.
```bash
sudo visudo
```

- Check user's sudo access
```bash
sudo -l
```
