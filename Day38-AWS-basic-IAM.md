**AWS IAM 

==> Create an IAM user with username of your own wish and grant EC2 Access. 
Launch your Linux instance through the IAM user that you created now and install jenkins and docker on your machine via single Shell Script.

Created user using IAM and attached EC2 full access. Created EC2 instance and logged in to the instance using terminal. Then installed jenkins and docker using shell script.

=======================

$ cat jenkin-docker.sh
#!/bin/bash

echo "Installing Jenkins"

sudo yum update –y

sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

sudo yum upgrade -y

#sudo amazon-linux-extras install java-openjdk11 -y

sudo dnf install java-11-amazon-corretto -y

sudo yum install jenkins -y

sudo systemctl enable jenkins

jenkins=`sudo systemctl status jenkins`

echo "Jenkins is installed $jenkins"

echo "==============================="

echo "Installing Docker"

sudo yum install docker -y

sudo systemctl enable docker.service

sudo systemctl start docker.service

status=`sudo systemctl status docker.service`


=======================
