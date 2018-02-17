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

## Port binding
`docker run -it --rm --name node -d -v %CD%:/src -w /src node:7.7.4-alpine node app.js` => -w working directory
`docker logs node`
`docker inspect node`
`docker run -it --rm --name node -d -v %CD%:/src -w /src node:7.7.4-alpine -p 8080:3000 node app.js` => -p host_port:container_port