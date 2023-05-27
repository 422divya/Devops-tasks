
1- Created the aws instance in same VPC as that of the Jenkins master to add it as the agent so the jenkisn job can run on it.

2- Configured the agent on the Jenkins master.

3- But while connecting the agent to the master it failed with below error:

/var/lib/jenkins/.ssh/known_hosts [SSH] No Known Hosts file was found at /var/lib/jenkins/.ssh/known_hosts. Please ensure one is created at this path and that Jenkins can read it.
Key exchange was not finished, connection is closed.
SSH Connection failed with IOException: "Key exchange was not finished, connection is closed.", retrying in 15 seconds. There are 10 more retries left.

4- Have copied the ec2-user public key in agent node. Configured the ssh passwordless connectivity between master and agent. Checked from CLI the passwordless connectivity and it was working

[root@source-instance ec2-user]$ ssh -i .ssh/id_rsa ec2-user@target-instance
 
Last login: Sat May 27 06:59:41 2023 from 43.207.151.187
[ec2-user@ip-target-instance ~]$ exit
logout
Connection to target-instance closed.

5- 
