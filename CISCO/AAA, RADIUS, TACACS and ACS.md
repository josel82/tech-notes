#### AAA (Authentication, Authorization, Accounting)
"It is a framework used to control and track access within a computer network. Common network protocols providing this functionality include TACACS+, RADIUS"
[https://en.wikipedia.org/wiki/AAA_(computer_security)]

#### ACS

"Cisco Access Control Server (ACS) is an **authentication, authorization, and accounting (AAA)** platform that lets you centrally manage access to network resources for a variety of access types, devices, and user groups."
[https://geek-university.com/what-is-cisco-acs/]

#### Configuration

The old way
```cisco
#Create a new model
Router(config)#aaa new-model

#Specify a backup login
Router(config)#username jose password cisco

Router(config)#tacacs-server host 10.1.1.1
Router(config)#tacacs-server key cisco
Router(config)#aaa authentication login default group tacacs+ local
```

The new way
```cisco
Router(config)#aaa new-model
Router(config)#username jose password cisco

#Register a new Tacacs server
Router(config)#tacacs server acs
Router(config-server-tacacs)#address ipv4 10.1.1.1
Router(config-server-tacacs)#key cisco
Router(config-server-tacacs)#exit

#Create server group and add the previously registered server
Router(config)#aaa group server tacacs+ acsgroup
Router(config-sg-tacacs)#server name acs
Router(config-sg-tacacs)#exit

#Finally we run:
Router(config)#aaa authentication login default group acs group local



```