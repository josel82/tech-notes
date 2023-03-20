# Paramiko
#Python #SSH #Networking 

"Paramiko is a pure-Python (3.6+) implementation of the SSHv2 protocol, providing both client and server functionality."
[Documentation](https://github.com/paramiko/paramiko)

## Installation
```linux
pip3 install paramiko
```

## How to use Paramiko
In this example, we have a script that connects to a cisco device via ssh.
```python
#!/usr/bin/env python3

import paramiko
import getpass
import time
  

HOST = input("Enter device IP Address: ")
username = input("Enter your username: ")
password = getpass.getpass()

print("Connecting to " + HOST)
client = paramiko.client.SSHClient()
client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
client.connect(HOST, username=username, password=password)

connection = client.invoke_shell()
connection.send("configure terminal\n")
connection.send("router ospf 1\n")
connection.send("network 0.0.0.0 255.255.255.255 area 0\n")
connection.send("exit\n")
connection.send("int loop 0\n")
connection.send("ip add 1.1.1.1 255.255.255.0\n")
connection.send("int loop 1\n")
connection.send("ip add 2.2.2.2 255.255.255.0\n")
connection.send("exit\n")
 

for n in range(2,21):
	print("Creating VLAN " + str(n))
	connection.send("vlan " + str(n) + "\n")
	connection.send("name Python_VLAN" + str(n) + "\n")
	time.sleep(1) 

connection.send("end\n")
time.sleep(1)
readoutput = connection.recv(65535)
print(readoutput.decode("ascii"))

client.close

```