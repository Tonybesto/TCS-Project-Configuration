## Installation Commands for Setting up Webservers, NGINX and Bation AMIs
# 

- create security group first
- create certificate
- create ALB
- create Launch template
- create Austocaling



# Bastion AMI Installation
```
sudo yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

sudo yum install -y dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm

sudo yum install wget vim python3 telnet htop git mysql net-tools chrony -y

sudo systemctl start chronyd

sudo systemctl enable chronyd
```
# Nginx AMI Installation 
```
sudo yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

sudo yum install -y dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm

sudo yum install wget vim python3 telnet htop git mysql net-tools chrony -y

sudo systemctl start chronyd

sudo systemctl enable chronyd
```
## Configure Selinux Policies For the Webservers and Nginx Servers
```
setsebool -P httpd_can_network_connect=1
setsebool -P httpd_can_network_connect_db=1
setsebool -P httpd_execmem=1
setsebool -P httpd_use_nfs 1
```
## This section will install Amazon EFS utils for mounting the target on the Elastic file system
```
git clone https://github.com/aws/efs-utils

cd efs-utils

sudo yum install -y make

sudo yum install -y rpm-build

sudo make rpm 

sudo yum install -y  ./build/amazon-efs-utils*rpm
```
### Seting up self-signed certificate for the Nginx instance
```
sudo mkdir /etc/ssl/private

sudo chmod 700 /etc/ssl/private

openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/TCS.key -out /etc/ssl/certs/TCS.crt

sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```
#

# Webserver AMI Installation 
```
sudo yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

sudo yum install -y dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm

sudo yum install wget vim python3 telnet htop git mysql net-tools chrony -y

sudo systemctl start chronyd

sudo systemctl enable chronyd
```
## Configure Selinux Policies for the Webservers and Nginx Servers
```
setsebool -P httpd_can_network_connect=1
setsebool -P httpd_can_network_connect_db=1
setsebool -P httpd_execmem=1
setsebool -P httpd_use_nfs 1
```
## This section will install Amazon EFS utils for mounting the target on the Elastic file system
```
git clone https://github.com/aws/efs-utils

cd efs-utils

sudo yum install -y make

sudo yum install -y rpm-build

sudo make rpm 

sudo yum install -y  ./build/amazon-efs-utils*rpm
```

## Seting up Self-Signed Certificate for the Apache Webserver Instance
```
sudo yum install -y mod_ssl

openssl req -newkey rsa:2048 -nodes -keyout /etc/pki/tls/private/TCS.key -x509 -days 365 -out /etc/pki/tls/certs/TCS.crt

vi /etc/httpd/conf.d/ssl.conf
```




# Login into the RDS instance and create  database for wordpress and tooling wordpress and tooling database
mysql -h tcs-database.cdqpbjkethv0.us-east-1.rds.amazonaws.com -u TCSadmin -p 

CREATE DATABASE toolingdb;
CREATE DATABASE wordpressdb;


# References
[IP ranges](https://ipinfo.io/ips)

[ssh-gent forwarding on mobaxterm](http://docs.gcc.rug.nl/hyperchicken/ssh-agent-forwarding-mobaxterm/)

[Nginx reverse proxy server](https://www.nginx.com/resources/glossary/reverse-proxy-server/)

[Underdstanding ec2 user data](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html)

[Manually installing the Amazon EFS client](https://docs.aws.amazon.com/efs/latest/ug/installing-amazon-efs-utils.html#installing-other-distro)

[creating target groups for AWS Loadbalancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-target-groups.html)

[Self-Signed SSL Certificate for Apache](https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-on-centos-8)

[Create a Self-Signed SSL Certificate for Nginx](https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-on-centos-7)
