1- Installed docker package and simply ran "docker run hello-world" which downloaded the hello-world image and created container.

2- docker inspect container_id  ==> Gives the details of the docker container 

3- docker stats container_id  ==> shows the resource usage by the container

4- docker top containeR_id   ==> to get the procees running inside the container

5- docker save image_name -o /tmp/docker-image  ==> to save the image to tar file

6-  docker load -i /tmp/docker-image  ==> To load the image from tar file
Loaded image: hello-world:latest
[root@ip-172-31-10-119 ~]# 
