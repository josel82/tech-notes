## Verifying IOS Code Integrity with MD5
#CISCO #IOS 

In Enable mode, run:
```
verify /md5 flash0:c2900-universalk9_npe-mz.SPA.150-1.M4.bin
```

This command will output an MD5 hash that you would then have to compare with the one published by CISCO. If they match, it means that the IOS image is legitimate.

You can also add the hash provided by CISCO to the end of this command and let it do the comparison for you:

```
verify /md5 flash0:c2900-universalk9_npe-mz.SPA.150-1.M4.bin 212334404eb71f6418fa6d7a8622de5f
```