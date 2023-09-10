# How to Install Open Day Ligth on Ubuntu Docker Container

## Update packet libraries
```bash
apt-get update
```

## Install Java
```bash
apt install openjdk-8-jre-headless 
```
Note: ODL version we intend to install requires JRE version 17 or higher

### Set JAVA_HOME
```bash
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64
```

## Install wget
```bash
apt-get install wget unzip -y
```

## Install unzip
```bash
apt-get install unzip
```

## Download OpenDayLight
[Download Page](https://docs.opendaylight.org/en/latest/downloads.html#)
```bash
wget https://nexus.opendaylight.org/content/repositories/public/org/opendaylight/integration/distribution-karaf/0.5.2-Boron-SR2/distribution-karaf-0.5.2-Boron-SR2.zip
```

## Unzip the downloaded file
```bash
unzip distribution-karaf-0.5.2-Boron-SR2.zip
```

## Start ODL
```
./distribution-karaf-0.5.2-Boron-SR2/bin/karaf
```

## Install ODL Features 
```bash
feature:install odl-restconf odl-l2switch-switch odl-mdsal-apidocs odl-dlux-all
```

## Web UI
You can access DLUX web ui from a browser at `http://ip-address:8181/index.html`