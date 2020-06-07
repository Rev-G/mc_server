UBUNTU
- login
- apt update
- apt upgrade
- ufw enable
- ufw allow 2255/tcp
## if needed to delete   ufw delete allow 22/tcp

## this is on my box
ssh-keygen -C "comment_or_email"
ssh-copy-id -i ~/.ssh/mykeyfile user@server -p {sshport}

## back on the server
vi /etc/ssh/sshd_config
PermitRootLogin no
ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no
AllowTcpForwarding no
X11Forwarding no
Port=4279

systemctl reload sshd

- install docker

Cloud at cost init (currently)  
1. local console as root
1. apt update
1. apt upgrade
1. update sshd_config (with Port, notrootlogon, and no x11forward)
1. systemctl restart sshd
1. adduser mrpalmer
1. usermod -aG sudo mrpalmer
1. ufw enable
1. ufw allow 2255/tcp

Now the automation can begin for Cloud at Cost  
## Install docker
```bash
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

```bash
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

```bash
sudo apt-get update  
sudo apt-get install docker-ce docker-ce-cli containerd.io
```


docker run -d -it -e EULA=TRUE -p 19132:19132/udp itzg/minecraft-bedrock-server

docker run -d -it --name bds-flat-creative \
  -e EULA=TRUE -e LEVEL_TYPE=flat -e GAMEMODE=creative \
  -p 19132:19132/udp itzg/minecraft-bedrock-server

#this is what i ran that worked
docker run -d -it --name=minecraft1 -e EULA=TRUE -p 19132:19132/udp -v /usr/local/share/minecraft/minecraft1:/data itzg/minecraft-bedrock-server