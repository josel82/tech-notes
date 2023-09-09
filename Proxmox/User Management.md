# User Management
#Proxmox #Virtualization 

[Source](https://www.youtube.com/watch?v=frnILOGmATs)

# User realm
In Proxmox we can add users in two different realms. Users created in the PAM realm are registered in the underlying system (nodes). This users are able to connect to the node via ssh.
On the other hand, users created in the Proxmox VE realm exist only in the proxmox context. These users are able to create and manage VMs from the proxmox GUI, but they can't access the nodes via ssh.

Here is how we create users in each realm:
## Linux PAM standard authentication
Go to **Datacenter > Permissions > Users** 
- Click on "Add"
- Fill up the form with the appropriate information, select Linux PAM standard authentication in the "Realm" dropdown menu and submit the form.
Next, add the user to the node:
- Select the node you want to add a user to, open up the console and add the new user with the `adduser` command:
```bash
adduser <username>
```

## Proxmox VE authentication server
Go to **Datacenter > Permissions > Users** 
- Click on "Add"
- Fill up the form with the appropriate information, select Proxmox VE authentication server in the "Realm" dropdown menu.
- Notice that this time we are asked for a password.
- Fill up the form and submit by clicking on the "add" button.

# User permissions
By default, newly created users are unable to see or do much. We can give users permissions as follows:
## Create a group
- Log in as root, Go to **Datacenter > Permissions > Groups** and click on "Add". Give the new group a name and submit the form.
- Next, on the main menu, click on "Permissions", then click on "Add", and select "Group Permission". A popup window appears, here you can specify the level of permission on the "Path" dropdown menu. Select the group you want to apply the permission to, select the appropriate role for the group. Click on "Add".

You can get further information on Roles at **Datacenter > Permissions > Roles** 
## Add user to the group
Go to **Datacenter > Permissions > Users** 
- Select the user, click on "Edit".
- Select the group you want the user to be part of on the "Group" dropdown menu.
- Click on "OK"
