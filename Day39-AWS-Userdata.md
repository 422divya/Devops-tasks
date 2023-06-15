**USER DATA**

Created EC2 instance by using user data from advance field. Added the shell script in user data so while first boot jenkins will be installed and we will get an instance with already installed jenkins.

After launching cross check script is stored in /var/lib/cloud/instancec/instance-id/. 

Checked the output log of script in /var/log/cloud-init-output.log

