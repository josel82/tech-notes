`Router#show running-config | redirect flash:/shruntest.cfg`

This command will copy the running configuration into a file `shrun test.cfg` and store it in flash

you can read this file as follows:

`Router#more flash:/shruntest.cfg`