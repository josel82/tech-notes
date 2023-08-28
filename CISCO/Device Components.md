Source: [Cisco Router Boot Sequence, Cisco Router POST (Power On Self Test)](https://www.omnisecu.com/cisco-certified-network-associate-ccna/cisco-router-boot-sequence.php)

- ### Flash 
	File System. Cisco IOS is stored here along with other files
- ### RAM
	Devices load the IOS to RAM during booting. The running configuration is stored in here.
- ### NVRAM
	The startup configuration is stored in here.
- ### ROM
	Contains the bootstrap program that Cisco devices use for starting other program such as the IOS. It also provides an eviroment **ROM Monitor** or ROMMON that can be used for password recovery, changing the configuration registry among other things. 

### Booting sequense
- Power On Self Test (POST)
- Start the Bootstrap program
	- check the configuration registrer and load the IOS accordingly (default: 0x2102 => Load the IOS from flash and load the startup config with console speed of 9600 bauds)
	- search IOS image in flash
	- if there's no IOS available in flash, try to find the IOS image via TFTP
	- if unsuccessful load ROMMON from ROM
- Load IOS to RAM
- Search for startup config in NVRAM and apply
	- if non is present, run configuratio wizard

