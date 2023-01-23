

**1- You have to do the same using Shell Script i.e using either Loops or command with start day and end day variables using arguments -
So Write a bash script createDirectories.sh that when the script is executed with three given arguments (one is directory name and second is start number of directories and third is the end number of directories ) it creates specified number of directories with a dynamic directory name.**

Example 1: When the script is executed as

./createDirectories.sh day 1 90

then it creates 90 directories as day1 day2 day3 .... day90

Example 2: When the script is executed as

./createDirectories.sh Movie 20 50 then it creates 50 directories as Movie20 Movie21 Movie23 ...Movie50


```
$ cat createDirectory.sh 
#!/bin/bash


# Enter the argument as the input. First argument as the directory, Second as the start number of directory and third argument is end number of directory.


for (( i=$2; i<=$3; i++))
do

output=`mkdir $1$i`

echo "directory created $output"
done
```

**2-Create a Script to backup all your work done till now.**

```
#!/bin/bash

source_dir=/home/ec2-user
destination_directory=/tmp

datetime=`date "+%Y-%m-%d-%H-%M-%S"`

backup_file=$destination_directory/$datetime.tgz

echo $backup_file

echo "Taking backup"
echo "==========================="
tar -czf $backup_file $source_dir

echo "Backup completed"
```

**3- Read About Cron and Crontab, to automate the backup Script
Cron is the system's main scheduler for running jobs or tasks unattended. A command called crontab allows the user to submit, edit or delete entries to cron. A crontab file is a user file that holds the scheduling information.**

### schedulded backup script every month on 1st day of month at 12:00 

```
$ crontab -l
0 12 1 * * bash /home/ec2-user/script/backup.sh >> /tmp/backup-cron-log.txt
```

**4-Create 2 users and just display their Usernames**
```
$ sudo useradd user1
$ sudo useradd user2
$ sudo passwd user1
$ sudo passwd user2

$ id user1
uid=5005(user1) gid=5006(user1) groups=5006(user1)
$ id user2
uid=5006(user2) gid=5007(user2) groups=5007(user2)
```

