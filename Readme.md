sudo apt update
sudo apt -y upgrade
reboot
sudo apt -y install curl openssh-server ca-certificates
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash

sudo apt install gitlab-ce

sudo apt install ufw
sudo ufw enable

sudo ufw allow "WWW Full"
sudo ufw allow OpenSSH
udo ufw allow 3306

sudo ufw status

sudo nano /etc/gitlab/gitlab.rb

## Edit the following line
external_url 'http://IP_of_the_vm'
Save the file and reload the configuration

sudo gitlab-ctl reconfigure

sudo apt install apt-transport-https ca-certificates curl gnupg2 software-properties-common
Add the GPG Key for the official docker repository

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
Update packages Database

sudo apt update
Install docker

sudo apt install docker-ce
Check if everything is ok

sudo systemctl status docker


sudo apt-get install gitlab-runner
Verify the installation is ok

systemctl status gitlab-runner
Registry the runner

# get the token
# http://IP_VM_GITLAB/root/t-nsa-700_back-end/-/settings/ci_cd

# BACK END RUNNER
# For build step
sudo gitlab-runner register -n --url http://IP_VM_GITLAB --registration-token ZvZxZtFzasUpyg9hyDVR --executor docker --description "T-NSA-700 Runner" --docker-image "docker:stable" --tag-list runner-back --docker-privileged

# FRONT END RUNNER
sudo gitlab-runner register -n --url http://IP_VM_GITLAB --registration-token t3F5KfEq8VfSbjoMWB6a --exe

udo apt install gnupg

cd /tmp
wget https://dev.mysql.com/get/mysql-apt-config_0.8.13-1_all.deb

sudo dpkg -i mysql-apt-config*

sudo apt update

sudo apt install mysql-server

ano /etc/my.cnf

bind-address        = 0.0.0.0

mysql -u root -p

CREATE USER 'dbuser'@'localhost' IDENTIFIED BY '12345678';
CREATE USER 'dbuser'@'%' IDENTIFIED BY '12345678';

GRANT ALL ON *.* TO 'dbuser'@'localhost';
GRANT ALL ON *.* TO 'dbuser'@'%';
flush privileges;
Firewall

sudo apt install ufw

ufw enable

ufw allow 3306
ufw allow 22
Test to connect remotly

mysql -u dbuser -h IP_VM_DB -p