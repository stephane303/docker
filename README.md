# Docker

* it's not a VM
* Image
    * Your starting point like a class 
    * What you produce as an output from a Dockefile
* Container
    * A running image
* Host
    * The machine docker is installed on 

## First example
`docker run -it --rm ubuntu /bin/bash`

## To the CLI
`docker run -it ubuntu /bin/bash`
-it => intertactive container

`docker ps`
=> list running container

`docker ps -a`
=> list stopped container

`docker start 49..`

`docker attach 49..`

`docker stop 49 ..`

`docker rm 49..`

`docker ps -a -q` return ids only

`docker rm $(docker ps -a -q)` delete stopped container

`docker run -it -d --rm --name ubuntu1 ubuntu /bin/bash` detatch mode + delete container when finished

`docker attach ubuntu1`
## Mount volume
`docker run -v %CD%:/files maxcunes/unrar -x -r Trunk.rar` => -v host_file:container_file

## Node example
`docker run -it --rm --name node node:7.7.4-alpine`
=> by default execute node

## Copy file local <-> container
 `docker cp . docker_informix_1:/opt/ibm/data/`

## Port binding
`docker run -it --rm --name node -d -v %CD%:/src -w /src node:7.7.4-alpine node app.js` => -w working directory

`docker logs node`

`docker inspect node`

`docker run -it --rm --name node -d -v %CD%:/src -w /src node:7.7.4-alpine -p 8080:3000 node app.js` => -p host_port:container_port

## Dockerfile
How to create an image in Docker
```docker
FROM node:7.7.4-alpine
EXPOSE 3000
RUN mkdir /src
COPY ap.js /src
WORKDIR /src
CMD node app.js
```
`docker build -t nodejs-app .` => -t = tag

`docker run --rm -p 8080:3000 -d nodejs-app`

## Docker Images
`docker images`

`docker rmi`


## Docker-Compose

Describe the environment docker-compose.yml
```docker
version: "3"
services:
    node:
        ports:
            - "8080:3000"
        networks:
            - webnet
        build:
            context:-/
            dockerfile: Dockerfile
networks:
    webnet:
```

Services are the container which you are going to start.

`docker-compose up node`

Show statistics.

`docker-compose stats`

Show config 

`docker-compose config`

## Docker swarm ##

Show where container are running
`docker stack ps <stack_name>`

Use docker cli on the swarm
`eval "$(<env.sh)" `

Deploy with multiple compose.yml (to be fixed, not working right now)

`docker stack deploy --compose-file docker-compose.yml  --compose-file docker-compose.deploy.yml  sylvia-edunil`

Workaround:

`docker-compose.exe -f docker-compose.yml  -f docker-compose.deploy.yml  config > stack.yml`

`docker stack deploy --compose-file stack.yml  sylvia-edunil`

Logs:

`docker service ps --no-trunc {serviceName}`

which will show errors with downloading images, mounting nfs volumes amongst others.

Not all errors can be found in the way described above. Another usefull tool is looking at the docker deamon logs which can be done the follwing way as explained on stackoverflow:

journalctl -u docker.service | tail -n 50 
It depends on your OS. Here are the few locations, with commands for few Operating Systems:

`Ubuntu (old using upstart ) - /var/log/upstart/docker.log

Ubuntu (new using systemd ) - journalctl -u docker.service

Boot2Docker - /var/log/docker.log

Debian GNU/Linux - /var/log/daemon.log

CentOS - /var/log/daemon.log | grep docker

CoreOS - journalctl -u docker.service

Fedora - journalctl -u docker.service

Red Hat Enterprise Linux Server - /var/log/messages | grep docker

OpenSuSE - journalctl -u docker.service

OSX - ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/log/d‌​ocker.log

Windows - Get-EventLog -LogName Application -Source Docker -After (Get-Date).AddMinutes(-5) | Sort-Object Time, as mentioned here.`


## Clean up ##

`docker system prune`









