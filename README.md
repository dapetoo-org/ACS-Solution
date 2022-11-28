
# Project Title

A brief description of what this project does and who it's for

- Create VPC
- Edit VPC and enable DNS Hostnames
- Create Internet Gateway and attach to the VPC created earlier
- Create subnets in the VPC (2 public and 4 private subnets)
- Create a Route Table (public and private route table)
- Associate subnets with the route table accordingly
- Edit the routes of the public route table by adding the internet gateway to the route to allow public internet access
- Create Elastic IP address 
- Create a NAT gateway in a public subnet and attach the EIP to it.
- Attach the NAT gateway to the private route table by clicking on edit route
- Create Security Groups
- Request for a public certificate from ACM
- Create Amazon Elastic File System and add a mount target
- Create Access Point from the EFS for wordpress and tooling
- Create key from KMS for RDS
- Create RDS subnet group for RDS database
- Create Database (RDS) select MySQL Engine
- Launch 3 EC2 instances to create AMI for Nginx, Bastion server and web server

Bastion AMI
```
sudo subscription-manager repos --enable codeready-builder-for-rhel-9-$(arch)-rpms
sudo dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
sudo dnf update -y
sudo dnf install -y dnf-utils http://rpms.remirepo.net/enterprise/remi-release-9.rpm
sudo dnf update --refresh
sudo yum install wget vim python3 telnet htop git mysql net-tools chrony -y
sudo systemctl start chronyd
sudo systemctl enable chronyd
```

Nginx Web server AMI

```
sudo subscription-manager repos --enable codeready-builder-for-rhel-9-$(arch)-rpms
sudo dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
sudo dnf update -y
sudo dnf install -y dnf-utils http://rpms.remirepo.net/enterprise/remi-release-9.rpm
sudo dnf update --refresh
sudo yum install wget vim python3 telnet htop git mysql net-tools chrony -y
sudo systemctl start chronyd
sudo systemctl enable chronyd

# Setup SELinux policy
setsebool -P httpd_can_network_connect=1
setsebool -P httpd_can_network_connect_db=1
setsebool -P httpd_execmem=1
setsebool -P httpd_use_nfs 1

# Installing self-signed certificate on the Nginx AMI
```
sudo mkdir /etc/ssl/private

sudo chmod 700 /etc/ssl/private

openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/ACS.key -out /etc/ssl/certs/ACS.crt

sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```

## Setup EFS utils
```
git clone https://github.com/aws/efs-utils

cd efs-utils

yum install -y make

yum install -y rpm-build

make rpm 

yum install -y  ./build/amazon-efs-utils*rpm
```


# Web server AMI Setup

```
sudo subscription-manager repos --enable codeready-builder-for-rhel-9-$(arch)-rpms
sudo dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
sudo dnf update -y
sudo dnf install -y dnf-utils http://rpms.remirepo.net/enterprise/remi-release-9.rpm
sudo dnf update --refresh
sudo yum install wget vim python3 telnet htop git mysql net-tools chrony -y
sudo systemctl start chronyd
sudo systemctl enable chronyd

sudo setsebool -P httpd_can_network_connect=1
sudo setsebool -P httpd_can_network_connect_db=1
sudo setsebool -P httpd_execmem=1
sudo setsebool -P httpd_use_nfs 1

# Generate self signed certificate
```

sudo yum install -y mod_ssl
```

Create Target group
Create Load Balancer
Create Launch Template
Create AutoScaling Group from the Launch Template
Create records in Route53 for tooling and wordpress


## Project Screenshots

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/01.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/02.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/03.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/04.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/05.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/06.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/07.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/08.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/09.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/10.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/11.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/12.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/13.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/14.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/15.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/16.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/17.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/18.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/19.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/20.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/21.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/22.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/23.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/24.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/25.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/26.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/27.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/28.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/29.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/30.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/31.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/32.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/33.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/34.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/35.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/36.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/37.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/38.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/39.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/40.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/41.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/42.png)

![Project Screenshots](https://github.com/scholarship-task/ACS-Solution/blob/main/screenshots/43.png)