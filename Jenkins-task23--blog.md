
Jenkins is the open source tool used for the continuous intergration , continuous development and continuous deployment.

It is developed using java. We can create a pipeline to build, test and deploy the code on development, test or production environments.


Configuring the ssh connectivity between Jenkins and Github

Create the ssh keys on the Jenkins server as shown below.

$ pwd
/home/ec2-user
[root@ip-172-31-10-119 ec2-user]# ls -larth .ssh/
total 4.0K

$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ec2-user/.ssh/id_rsa):  
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/ec2-user/.ssh/id_rsa
Your public key has been saved in /home/ec2-user/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:Xb78l4SfQL6URHVYslWDsRuOLNm2O0XqW4xxAjUFyK4 ec2-user@ip-172-31-10-119.ap-northeast-1.compute.internal
The key's randomart image is:
+---[RSA 3072]----+
|        . .+oo==*|
|         o. .oo+o|
|        ..  oo.  |
|         o=oo+o  |
|        So.BB+o  |
|       E  ooBO . |
|          .o=o= o|
|           ooo +.|
|           oo .. |
+----[SHA256]-----+

public and private keys are now generated successfully.

Now copy the public key generated in the github as below:

1- Login to github.

2- Navigate to your profile on the top right corner ==> Go in Settings ==> SSH and GPG keys ==> Click on New SSH key ==> In Key box paste the copied public key that was generated in above steps.


Configuring the credentials in jenkins:

In jenkins we will configure the credentials of the github. Here we are using the "SSH Username with private key option" in jenkins.

Below are the steps to configure the credentials for the GitHub in Jenkins:

1- Login to Jenkins.

2- Go in Manage Jenkins 

3- Click on Credentials and then Add credentials

4- New credentials page will be opened as show below.

5- Select "SSH Username with private key" from drop down list in kind option.

6- You can provide the ID or else can leave it as blank also description is optional.

7- Enter the username for which the ssh keys were created. In my case I have created keys for ec2-user.

8- Select "Enter directly" option under private key and copy the private key from the server and click on save.

9- Now jenkins can communicate with github using passwordless ssh connectivity.



Task2- USed docker-compose file to create multiple container. But at first receivd below error while running Jenkins jobs.


Started by user Divya
Running as SYSTEM
Building in workspace /var/lib/jenkins/workspace/docker-compose
The recommended git tool is: NONE
No credentials specified
Cloning the remote Git repository
Cloning repository https://github.com/422divya/Docker-compose.git
 > git init /var/lib/jenkins/workspace/docker-compose # timeout=10
Fetching upstream changes from https://github.com/422divya/Docker-compose.git
 > git --version # timeout=10
 > git --version # 'git version 2.39.2'
 > git fetch --tags --force --progress -- https://github.com/422divya/Docker-compose.git +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git config remote.origin.url https://github.com/422divya/Docker-compose.git # timeout=10
 > git config --add remote.origin.fetch +refs/heads/*:refs/remotes/origin/* # timeout=10
Avoid second fetch
 > git rev-parse refs/remotes/origin/master^{commit} # timeout=10
 > git rev-parse origin/master^{commit} # timeout=10
ERROR: Couldn't find any revision to build. Verify the repository and branch configuration for this job.
Finished: FAILURE

After changing the jenkins job configuration it got fixed. Issue was under Sorce code management "Branch to build was mentioned as master" due to which while fetching the code from the github repository it was unable to find it as the code was in main branch. After changing from master to main code was executed successfully.
