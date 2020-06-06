## Welcome

using some steps detailed here for base config of our centos 7 server

https://medium.com/@saeedrz/5-steps-to-hardening-your-server-centos-7-25e1851c8204

Centos7
yum install firewalld

Centos8
dnf install firewalld

systemctl enable firewalld --now
firewall-cmd --set-default-zone=public
firewall-cmd --zone=public --set-target=DROP --permanent
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
Port=4279

systemctl reload sshd
