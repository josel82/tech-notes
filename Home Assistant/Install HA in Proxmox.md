# Install HA in Proxmox
#HomeAssistant #Linux #IOT

## Create a new VM
1. Give it a name and an ID.
![[Home Assistant/Pictures/create-vm-01.png]]

2. Since we are going to be importing a virtual disk, select "Do not use any media". Keep Linux as Guest OS.
![[Home Assistant/Pictures/create-vm-02.png]]

3. Next, set the following values in the System section. Make sure you uncheck the "Pre-Enroll keys" option.
![[Home Assistant/Pictures/create-vm-03.png]]

4. Since we are going to import a virtual disk from the Home Assistan website, we want to delete the default disk in the following section. Click on the delete button on the left side of the window, beside "scsi0".
![[Home Assistant/Pictures/create-vm-04.png]]

The click on "Next".
![[Home Assistant/Pictures/create-vm-05.png]]

5. Next, select 2 cores as specified in the [Documentation](https://www.home-assistant.io/installation/linux).
![[Home Assistant/Pictures/create-vm-06.png]]

6. Set the memory to 2GB as per the [Documentation](https://www.home-assistant.io/installation/linux).
![[Home Assistant/Pictures/create-vm-07.png]]

7. On the Network section, select the network Bridge you want to connect this VM to and add a VLAN tag in case you want this VM to be in a specific subnet. Make sure the selected network bridge is VLAN aware and set up accordingly.
![[Home Assistant/Pictures/create-vm-08.png]]

8. Finally confirm all the settings and hit "Finish".
![[create-vm-09.png]]

## Import HA virtual disk
1. Go to: https://www.home-assistant.io/installation/linux.
2. Right click on "KVM" and copy the link.
![[link.png]]

3. Back in Proxmox, log into the node shell and run the following command:
```bash
wget https://github.com/home-assistant/operating-system/releases/download/9.5/haos_ova-9.5.qcow2.xz
```
This will download Home Assistant virtual disk to the home directory.

4. Decompress the file.
```bash
xz -d -v haos_ova-9.5.qcow2.xz
```

5. Import the disk into the VM
```bash
qm importdisk 200 haos_ova-9.5.qcow2 local-lvm --format qcow2
```
Once this is done. The imported disk will appear in the VM as an unused disk.

6. Now that the disk has been succesfully imported, you can delete the `qcow2` file left in the home directory.
```bash
rm haos_ova-9.5.qcow2
```

7. Go to the Virtual Machine Menu and select "Hardware". In here you can add the imported disk by clicking on it, then clicking on edit.
![[hardware.png]]

A window will pop up. Click on "Add".
![[add-disk.png]]

8. Finally, change the boot order. On the VM menu go to Options > Boot order. Check the imported disk and drag it to the top.


## Start the VM

Hit the Start button and let the VM boot up. Once its done booting up it will show a banner with general information about the system, grab the IP address.
![[banner.png]]

Open up you web browser and go to `http://192.168.2.180:8123` 
Replace the IPv4 address with your VMs address.

A sign up form should appear. Now you should proceed creating a Home Assistant account [Follow these instructions](https://www.home-assistant.io/getting-started/onboarding/)

