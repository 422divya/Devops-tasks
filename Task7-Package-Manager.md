# Package Manager and Systemctl

#### Installed Docker and Jenkins using yum package manager

==> sudo yum install docker

#### To install Jenkins:

==> sudo yum update –y

sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo  <== Adding Jenkins repository to system

sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key  <== Importing the jenkins key

sudo amazon-linux-extras install java-openjdk11 -y  <== Installing java

sudo yum install jenkins -y

#### Reference Link To install jenkins:

https://www.jenkins.io/doc/tutorials/tutorial-for-installing-jenkins-on-AWS/


#### Enabled and started Docker and Jenkins services using systemctl:

==>
sudo systemctl enable docker
sudo systemctl start docker

sudo systemctl enable jenkins
sudo systemctl start jenkins
