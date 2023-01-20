
# Linux Commands

**To view what is written in a file**

`cat file_name` : This command will print the output of the file on screen.

**To change the access permissions of files**

We can give read, write and execute permissions to file/directories. 

Below is the number code for the permission type:

```
r=read = 4 : To view file
w=write = 2 : To modify or write to the file
x=execute = 1 : Can execute the file/script change to directory
```

`chmod 777 file_name` : It will give full permission to the file/directory

`chmod -R 755` directory_name : It will recurcively change permissions directory and of files/subdirectory in that directory. 

`chown owner:group file.txt` : To chnage the ownership of the file/directory

`chgrp group filename` : To chnage the group ownership of the file/directory

**To remove a directory/ Folder**

`rmdir dir_name` : To remove/delete the directory

`rm -rf dir_name` : To remove/delete directory when directory is not empty. This will delelte all the content of directory first and then delete directory.

`rm file_name`: To delete file.

**To create a fruits.txt file and to view the content**

```
[root@ip-XXX ec2-user]# touch fruits.txt
[root@ip-XXX ec2-user]# vim fruits.txt 
[root@ip-XXX ec2-user]# cat fruits.txt 
This is test file
[root@ip-1XXX ec2-user]# 
```

**Created file devops.txt with below content**

```
# cat devops.txt 
Apple
Mango
Banana
Cherry
Kiwi
Orange
```

**To Show only bottom three fruits from the file**

```
# cat devops.txt |tail -3
Cherry
Kiwi
Orange
```

**To create another file Colors.txt with below content:**

```
# cat colors.txt 
Red
Pink
White
Black
Blue
Orange
Purple
Grey
```

**To get the differece from both the files:**

```
# diff devops.txt colors.txt 
1,5c1,5
< Apple
< Mango
< Banana
< Cherry
< Kiwi
---
> Red
> Pink
> White
> Black
> Blue
6a7,8
> Purple
> Grey
```

From above by using diff command we can get the differences in the both the files. 

```
`a` : Add
`c` :change
`d` : Delete
```

1,5c1,5 means line 1 to 5 in first file devops.txt needs to be replaced/changed to match line 1 to 5 in second file colors.txt. The changes need to be done are replace content starting with symbol `<` with content starting with `>` sign.

So above output means in devops.txt `<` sign means need to delete that content and `>` sign indicates to add that content in devops.txt to make it same as of colors.txt.

6a7,8 means in line 6 of devops.txt file add  7th and 8th line from colors.txt
