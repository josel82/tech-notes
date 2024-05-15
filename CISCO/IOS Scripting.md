# IOS scripting

## tclsh
```
router#tclsh
router(tcl)#
```

### for loop ping
```
foreach addresses {
172.20.1.1
172.20.1.2
172.20.1.3
172.20.1.4
} { ping $addresses rep 3 }
```

