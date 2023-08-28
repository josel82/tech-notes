- Select and download the correct IOS image
	www.cisco.com > support > software download
	
- Verify connectivity
	ping the TFTP's IP address
	
- Verify that the router has suficient flash memory space
	run `sh flash` from the priviledge mode and check flash memory size
	
- Copy the IOS from the TFTP server to the router
	[[File system#^f6a129]]
	
- Configure the router to boot
	`Router(config)#boot system flash:c2900-universalk9_npe-mz.SPA.150-1.M4.bin`
	
- Reload the router
	save the running configuration `Router#copy run start`
	reload the router `Router#reload`


### Download IOS from 
www.cisco.com > support > software download

