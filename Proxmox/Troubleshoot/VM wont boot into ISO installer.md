# VM wont boot into ISO installer
#Proxmox #Virtualization 

[Proxmox forum](https://forum.proxmox.com/threads/help-failed-to-start-boot0001-uefi-qemu-dvd-rom-time-out.83521/)
## Problem
UEFI fails to boot from ISO uploaded into DVD-ROM device. Output says "Access Denied"

## Solution
Hit ESC right after the "Startup boot options" message. This will bring you to the UEFI. In there you need to disable the Secure Boot feature.