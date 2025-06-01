source: https://www.youtube.com/watch?v=yys2o0H-Kpc
1. Download IOS image from https://software.cisco.com/download
2. Copy the image into the switch's flash, the easiest way to do this is by getting the image in a USB stick, then connecting the USB stick to the switch and copying the file as follows:
```
copy usbflash0:cat9k_iosxe.17.12.04.SPA.bin flash:
```
3. Verify the image has copied over:
```
dir flash:
```
4. Install the image:
```
request platform software package install switch 1 file flash:cat9k_iosxe.17.12.04.SPA.bin
```
5. Once the image is successfully installed, reboot the switch so it loads the new software:
```
reload
```