**Creating the volume and binding it to the container so that the data can be saved in hosts volume as well. If container goed down or deleted the data is saved in the volume on hosts.**
**Also same volume can be used on many containers.**
 
 
 $ cat /home/ec2-user/docker-mount/test 
test
[root@ip-172-31-10-119 Docker]# cat docker-compose.yml 
version: '3.3'
services:
  web:
    image: httpd:latest
    ports:
      - 80:80
    volumes:
      - type: bind
        source: /home/ec2-user/docker-mount
        target: /app


  db:
    image: postgres:latest
    ports:
      - 5432:5432
    environment:
       POSTGRES_PASSWORD: test@123

volumes:
  docker_vol:
