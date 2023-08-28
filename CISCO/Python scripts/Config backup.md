my_switches
```
192.168.1.72
192.168.1.73
192.168.1.74
192.168.1.75
192.168.1.76
```

switchBackup.py
```pyhton3
import getpass
import telnetlib

user = raw_input("Enter your telnet username: ")
password = getpass.getpass()

f = open("my_switches")

for line in f:
    print f"Getting running config from switch {line}"
    HOST = line.strip()
    tn = telnetlib.Telnet(HOST)
    
    tn.read_until("Username: ")
    tn.write("\n")
    if password:
        tn.read_until("Password: ")
        tn.write("\n")
        
    tn.write("terminal length 0\n")
    tn.write("show run\n")
    tn.write("exit\n")
    
    readoutput = tn.read_all()
    saveoutput = open(f"switch_{HOST}")
    saveoutput.write(readoutput)
    saveoutput.close()
	
```

