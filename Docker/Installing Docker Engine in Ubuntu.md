# Installing Docker Engine in Ubuntu
#Docker #DevOps 

[Documentation](https://docs.docker.com/engine/install/ubuntu/)


## Install Docker Engine
```bash
sudo apt update
```

```bash 
sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
```

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

```bash
sudo apt update
```

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Check that Docker has been installed correctly
```bash
sudo docker --version
```

```bash
sudo docker run hello-world 
```

### Add user to Docker group
```bash
sudo usermod -aG docker $USER
```

## Install Docker Compose
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
```

