
# Installation of Docker Enginee on Ubuntu 

## Supported OS :

- Ubuntu Jammy 22.04 (LTS)
- Ubuntu Focal 20.04 (LTS)
- Ubuntu Bionic 18.04 (LTS) 

## Step By Step Installation :

1. Uninstall Old Version 

Older versions of Docker went by the names of docker, docker.io, or docker-engine. Uninstall any such older versions before attempting to install a new version,

```
sudo apt-get remove docker docker-engine docker.io containerd runc
```

2.  Install the Prerequisites 

```
sudo apt-get update 
sudo apt-get -y upgrade
sudo apt-get -y install ca-certificates curl gnupg lsb-release
```

3. Set up the repository & Official GPG Key

```
sudo mkdir -p /etc/apt/keyrings

# Add Official GPG Key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Set up the repository
echo deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

4. Install Docker Engine

```

# Install Latest Version
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

OR 

# Install Specific Version 

# Check list of available versions 
apt-cache madison docker-ce | awk '{ print $3 }'

# Specific Version Here
VERSION_STRING=5:20.10.13~3-0~ubuntu-jammy
sudo apt-get install docker-ce=$VERSION_STRING docker-ce-cli=$VERSION_STRING containerd.io docker-compose-plugin
```

5. Create `docker` group and add your user to `docker` group

```
# Create the `docker` group
sudo groupadd docker

# Add your user to the `docker` group
sudo usermod -aG docker $USER
```

6. Restart the system & verfiy that you can run `docker` commands without sudo.

```
# Restart Command(You can skip this and restart it manually)
sudo reboot 

# Verify 
docker run hello-world
```