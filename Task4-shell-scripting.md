# Shell Scripting

**Explain in your own words and examples, what is Shell Scripting for DevOps.**

==> Shell scripting is the sequence of commands that is executed on the shell like bash,sh,ksh etc. 
In Devops shell scripting can be useful to automate the various activities like creating script to monitor the system, Installing multiplepackages, creating users on linux system, configguring system etc.

**What is #!/bin/bash? can we write #!/bin/sh as well?**

==> `#!/bin/bash` is written at top of the shell script. It informs which shell to use to operating system, in this case it's the bash shell, so when running the script it will use bash shell. Bash is the `Bourne Again Shell`.  Shell which is an interpreter to communicate with the kernel. Shell take input in form of command which is in human readable language and convert it into machine understandable language.

We can write the ` #!/bin/sh` as well which is the bourne shell. If we mentione this while writing script the shell will run script using sh shell.

**Write a Shell Script which prints I will complete #90DaysOofDevOps challenge**

```
$ cat printmsg.sh 
#!/bin/bash

echo "I will complete #90DaysOofDevOps challenge"

Output:

$ sh printmsg.sh 
I will complete #90DaysOofDevOps challenge
```

**Write a Shell Script to take user input, input from arguments and print the variables.**

```
$ cat argument.sh 
#!/bin/bash

echo $1

$ sh argument.sh hello
hello
```

**Write an Example of If else in Shell Scripting by comparing 2 numbers**

```
 cat compare_two_numbers.sh 
#!/bin/bash 

echo "Enter two numbers to compare"

read num1
read num2

if [ $num1 -gt $num2 ]
then    
        echo "$num1 is greater than $num2"
        
else    
        echo "$num2 is greater than $num1"
        
 **OUTPUT**
 
 $ sudo sh compare_two_numbers.sh 
Enter two numbers to compare
3
1
3 is greater than 1

$ sudo sh compare_two_numbers.sh 
Enter two numbers to compare
10
33
33 is greater than 10
```
**Reverse the string**
```
$ cat reverse.sh 
#!/bin/bash

echo "enter sting again"
read text

output=$(echo $text|rev)

echo $output
```
