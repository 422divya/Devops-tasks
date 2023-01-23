**File and Directory permission in Linux**

==> Created files and dircetory checked there permission using ls -lrth. Changed the permission of it using chmod.

r=read=4
w=write=2
x=execute=1

**ACL=Access Control List**

==> ACL is also use to set the permission on files and directories. We can get permission details of files and directories using ``getfacl``` command and can set the permission using ```setfacl``` permission.

```
$ getfacl /home/ec2-user/
getfacl: Removing leading '/' from absolute path names
# file: home/ec2-user/
# owner: ec2-user
# group: ec2-user
user::rwx
user:test:rwx
group::---
mask::rwx
other::---

$ setfacl -m u:user1:r-x /home/ec2-user/   <== Set the permssion for the user1 to access ec2-user home directory.

$ getfacl /home/ec2-user/
getfacl: Removing leading '/' from absolute path names
# file: home/ec2-user/
# owner: ec2-user
# group: ec2-user
user::rwx
user:test:rwx
user:user1:r-x
group::---
mask::rwx
other::---
```
