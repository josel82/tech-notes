switchConfig01.py
```python3
import getpass
import sys
import telnetlib

user = raw_input("Enter your telnet username: ")
password = getpass.getpass()

for n in range(72,77):
    HOST = f"192.169.1.7{n}"
    tn = telnetlib.Telnet(HOST)
    
    tn.read_until("Username: ")
    tn.write("\n")
    if password:
        tn.read_until("Password: ")
        tn.write("\n")
        
    tn.write("conf t\n")
    
    for n in range(2,6)
	    tn.write(f"vlan {n}\n")
	    tn.write(f"name Python_VLAN_{n}\n")
	    
	tn.write("end\n")
	tn.write("wr\n")
	tn.write("exit\n")
	
	print tn.read_all()

```


#### Better approach

sw_addresses
```
192.168.1.72
192.168.1.73
192.168.1.74
192.168.1.75
192.168.1.76
```


switchConfig02.py
```python3
import getpass
import sys
import telnetlib

user = raw_input("Enter your telnet username: ")
password = getpass.getpass()

f = open("sw_addresses")

for line in f:
    print f"configuring switch {line}"
    HOST = line
    tn = telnetlib.Telnet(HOST)
    
    tn.read_until("Username: ")
    tn.write("\n")
    if password:
        tn.read_until("Password: ")
        tn.write("\n")
        
    tn.write("conf t\n")
    
    for n in range(2,6)
	    tn.write(f"vlan {n}\n")
	    tn.write(f"name Python_VLAN_{n}\n")
	    
	tn.write("end\n")
	tn.write("wr\n")
	tn.write("exit\n")
	
	print tn.read_all()
```