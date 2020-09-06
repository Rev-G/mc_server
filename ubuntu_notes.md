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
Port=2255

systemctl reload sshd

- install docker

Cloud at cost init (currently)  
1. local console as root
1. apt update
1. apt upgrade
1. update sshd_config (with Port, notrootlogon, and no x11forward)
1. systemctl restart sshd
1. adduser {username}
1. usermod -aG sudo {username}
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

#should rename this one to minecraft-testbed. 
docker run -d -it --name=minecraft1 -e EULA=TRUE -e SERVER_NAME="minecraft1" -e SERVER_NAME="Minecraft 1" -p 19132:19132/udp -v /usr/local/share/minecraft/minecraft1:/data itzg/minecraft-bedrock-server

#should rename this one to minecraft-creative. 
docker run -d -it --name=minecraft2 -e EULA=TRUE -e GAMEMODE=creative -e ALLOW_CHEATS=true -e SERVER_NAME="Minecraft 2" -e SERVER_PORT=19142 -e LEVEL_NAME="Bedrock_Mine" -e LEVEL_SEED="2048971879" -p 19142:19142/udp -v /usr/local/share/minecraft/minecraft2:/data itzg/minecraft-bedrock-server

docker run -d -it --name=minecraft-survival -e EULA=TRUE -e GAMEMODE=survival -e DIFFICULTY=normal -e SERVER_NAME="Minecraft Survival" -e SERVER_PORT=19152 -e LEVEL_NAME="Bedrock_Survival" -e LEVEL_SEED="625452737" -p 19152:19152/udp -v /usr/local/share/minecraft/minecraft-survival:/data itzg/minecraft-bedrock-server

docker run -d -it --name=minecraft-flat -e EULA=TRUE -e LEVEL_TYPE=flat -e GAMEMODE=creative -e ALLOW_CHEATS=true -e SERVER_NAME="Minecraft Flat" -e SERVER_PORT=19162 -e LEVEL_NAME="Bedrock_Flat_Mine" -p 19162:19162/udp -v /usr/local/share/minecraft/minecraft-flat:/data itzg/minecraft-bedrock-server

docker run -d -it --name=jungle-survival -e EULA=TRUE -e GAMEMODE=survival -e DIFFICULTY=normal -e SERVER_NAME="Jungle Survival" -e SERVER_PORT=19172 -e LEVEL_NAME="Jungle_Survival" -e LEVEL_SEED="9144" -p 19172:19172/udp -v /usr/local/share/minecraft/jungle-survival:/data itzg/minecraft-bedrock-server


minecraft1
45.62.216.96
19132

minecraft2
45.62.216.96
19142

mc survival
45.62.216.96
19152

mc flat
45.62.216.96
19162

mc jungle
45.62.216.96
19172

sudo tar -czvf /home/mrpalmer/minecraft-backups/mcsurvival.zip whitelist.json server.properties worlds
