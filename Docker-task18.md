**Create docker compose file to create container

1- Created below docker compose file to create container for apache and postgres db container.

# cat docker-compose.yml 
version: '3.3'
services:
  web:
    image: httpd:latest
    ports:
      - 80:80

  db:
    image: postgres:latest
    ports:
      - 5432:5432
    environment:
       POSTGRES_PASSWORD: test@123

# docker-compose up
Creating network "docker_default" with the default driver
Pulling web (httpd:latest)...
latest: Pulling from library/httpd
9e3ea8720c6d: Pull complete
35c516cd98eb: Pull complete
3050fa5900bc: Pull complete
f14b7012c455: Pull complete
014a91cb6174: Pull complete
Digest: sha256:90254ccc7352e1a5c8d1e4cdab2a032cefac9fd5d4d632ca003a2943c9a9b0a3
Status: Downloaded newer image for httpd:latest
Pulling db (postgres:latest)...
latest: Pulling from library/postgres
9e3ea8720c6d: Already exists
7782b3e1be4b: Pull complete
247ec4ff783a: Pull complete
f7ead6900700: Pull complete
e7afdbe9a191: Pull complete
3ef71fe7cece: Pull complete
1459ebb56be5: Pull complete
3595124f6861: Pull complete
26ececf90b13: Pull complete
f4809920222b: Pull complete
c3f8fa066d45: Pull complete
01bbc0ffaa2f: Pull complete
feedb98bec2e: Pull complete
Digest: sha256:8d45935fb783e72c871072e9eb72ee8c817a9eaf25c405b0e62526b14191368d
Status: Downloaded newer image for postgres:latest
Creating docker_web_1 ... done
Creating docker_db_1  ... done
Attaching to docker_db_1, docker_web_1
web_1  | AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.18.0.2. Set the 'ServerName' directive globally to suppress this message
web_1  | AH00558: httpd: Could not reliably determine the server's fully qualified domain name, using 172.18.0.2. Set the 'ServerName' directive globally to suppress this message
web_1  | [Sat May 20 14:19:44.215849 2023] [mpm_event:notice] [pid 1:tid 140685361618240] AH00489: Apache/2.4.57 (Unix) configured -- resuming normal operations
web_1  | [Sat May 20 14:19:44.217194 2023] [core:notice] [pid 1:tid 140685361618240] AH00094: Command line: 'httpd -D FOREGROUND'
db_1   | The files belonging to this database system will be owned by user "postgres".


docker-compose down  <<= It will delete the containers
