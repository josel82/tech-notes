# How to create an ISO image from a folder
#MacOS #ISO 

1. Open **Disk Utility** and  go to **File > New Image > Image from Folder**, then select the folder you want to turn into and ISO image.
2. Give the file a name and select the destination folder, then on the **Image Format** dropdown select DVD/CD Master (Keep it without encryption). This will generate a cdr image.
3. Convert the cdr image into and ISO image. From the directory were the .cdr image is located, run the following command:

```zsh
hdiutil makehybrid -iso -joliet -o file_name.iso file_name.cdr
```
