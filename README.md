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


