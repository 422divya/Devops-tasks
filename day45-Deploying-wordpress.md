**Deploying wordpress on AWS**

1- Created EC2 instance

2- Created MYSQL DB.

3- Installed wordpress on EC2. Downoaded the wordpress code and copied it to /var/www/html path.

4- Then installed php package.

5- Tried to access the wordpress but it failed with below error.

http://13.231.254.245/wp-admin/install.php
The database server could be connected to (which means your username and password is okay) but the db1 database could not be selected.

6- On checking found db name was different which is 'mysqldb' on checking in DB created on AWS and 'db1' is identifier of DB.


https://aws.amazon.com/getting-started/hands-on/deploy-wordpress-with-amazon-rds/
