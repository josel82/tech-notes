1. Log in to the CISCO device.

2. Go to global configuration mode.
	`switch>enable`
	`shitch#conf t`

3. Enable password encryption
	`switch(config)#service password-encryption`

4. Create an encrypted 'enable password'
	`switch(config)#enable secret cisco123`

5. Declare a domain name
	`switch(config)#ip domain-name lab.cisco.com`

6. Generate a RSA encryption key
	`switch(config)#crypto key generate rsa`

7. Crate a username and password
	`switch(config)#username admin password cisco`

8. Configure virtual interfaces for remote acces vis SSH
	`switch(config)#line vty 0 4`
	`switch(config-line)#login local`
	`switch(config-line)#transport input ssh`
	`switch(config-line)#exit`

9. Configure SSH
	`switch(config)#ip ssh version 2`
	`switch(config)#ip ssh time-out 120`
	`switch(config)#ip ssh authentication-retries 3`

10. Setup a password for access via console
	`switch(config)#line console 0`
	`switch(config-line)#password cisco`
	`switch(config-line)#login`
	`switch(config-line)#exit`

11. Save changes
	`switch(config)#exit
	`switch#copy running-config startup-config