

You have to do the same using Shell Script i.e using either Loops or command with start day and end day variables using arguments -
So Write a bash script createDirectories.sh that when the script is executed with three given arguments (one is directory name and second is start number of directories and third is the end number of directories ) it creates specified number of directories with a dynamic directory name.

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
