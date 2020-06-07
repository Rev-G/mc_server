## Welcome

using some steps detailed here for base config of our centos 7 server

https://medium.com/@saeedrz/5-steps-to-hardening-your-server-centos-7-25e1851c8204

Centos7
yum install firewalld
#stuff needed for selinux
yum -y install policycoreutils-python
semanage port -a -t ssh_port_t -p tcp 2211
yum install -y yum-utils
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
yum install docker-ce docker-ce-cli containerd.io

Centos8
dnf install firewalld

systemctl enable firewalld --now
firewall-cmd --set-default-zone=public
firewall-cmd --zone=public --set-target=DROP --permanent
## ssh-mod changes the port
cp ssh-mod.xml /usr/lib/firewalld/services/ssh-mod.xml
firewall-cmd --zone=public --remove-service=ssh --permanent
firewall-cmd --zone=public --add-service=ssh-mod --permanent
** Need to updated to not allow zone hoping in the config

adduser mrpalmer
passwd mrpalmer
usermod -aG wheel mrpalmer

ssh-keygen -C "comment_or_email"
ssh-copy-id -i ~/.ssh/mykeyfile user@server -p {sshport}

vi /etc/ssh/sshd_config
PermitRootLogin no
ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no
AllowTcpForwarding no
X11Forwarding no
Port=2255

systemctl reload sshd

UBUNTU
- login
- apt update
- apt upgrade
- ufw enable
- ufw allow 2255/tcp
## if needed to delete   ufw delete allow 22/tcp
- adduser mrpalmer
- passwd mrpalmer
- usermod -aG wheel mrpalmer

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







