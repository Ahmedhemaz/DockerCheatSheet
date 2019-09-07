# Table of content:
- [Docker Introduction](#Docker-Introduction)
- [Manipulating Containers with the Docker Client](#Manipulating-Containers-with-the-Docker-Client)
- [Building Custom Images Through Docker Server](#Building-Custom-Images-Through-Docker-Server)
- [Building multiple containers with "Docker-compose"](#Building-multiple-containers-with-"Docker-compose")
___
# Docker Introduction
- [run Docker image](#1--run-docker-image)
- [run command from container](#2--to-run-command-from-container)
- [list all running containers](#3--list-all-running-containers-on-machine)
- [list all containers ever created on machine](#4--list-all-containers-ever-created-on-machine)
- [stop running container](#5--stop-running-container)
___
### 1- run Docker image:
    docker run <image-name>
- that will check image build cache if image is not there "Docker-server" will get that image from "Docker-HUB" then run the container
- you can run container in back ground using:
      
      docker run -d <image-name>
___
### 2- to run command from container:
    docker run <image-name> <command-wanna-to-excute>
- command must be in file system snap shot of the image
___
### 3- list all running containers on machine:
    docker ps  
___
### 4- list all containers ever created on machine:
    docker ps --all
___
### 5- stop running container:
      docker stop <container-id>
___

# Manipulating Containers with the Docker Client

- [Create Docker container](#1--Create-Docker-container)
- [Start Docker container](#2--Start-Docker-container)
- [Remove All Stopped containers](#3--Remove-All-Stopped-containers)
- [Get Docker container log](#4--Get-Docker-container-log)
- [Stop Docker container](#5--Stop-Docker-container)
- [Kill Docker container](#6--Kill-Docker-container)
- [Run Command inside Docker container](#7--Run-Command-inside-Docker-container)
- [Run Terminal inside Docker container](#8--Run-Terminal-inside-Docker-container)
- [Start Docker container with Terminal](#9--Start-Docker-container-with-Terminal)
- [Start Docker container with Port Mapping](#10--Start-Docker-container-with-Port-Mapping)
___
### 1- Create Docker container:
    docker create <image-name>
- that will check image build cache if image is not there "Docker-server" will get that image from "Docker-HUB" then will load file system snap shot to isolated container
___
### 2- Start Docker container:
    docker start <Container-id> 
- run the startup command of the created container
- can't override old default(startup) command of existed container
- starting docker container with that command will return the container id
#### To watch the output of the container to the terminal:
    docker start -a <Container-id> 
## *Docker run:
    docker run = docker create + docker start
___
### 3- Remove All Stopped containers:
    docker system prune 
- remove all stopped containers
- remove all dangling images
- remove all networks not used by one container
- remove all build cache images (need to download image again)
___
### 4- Get Docker container log:
    docker logs <Container-id>
- get all records of logs that have been emitted from that container
___
### 5- Stop Docker container:
    docker stop <Container-id>
- will send stop signal to  process in container and if exceeded 10s runs docker kill (Kill the container)
___
### 6- Kill Docker container:
    docker kill <Container-id>
- will send kill signal to process in container which will kill the container immediately
___
### 7- Run Command inside Docker container:
    docker exec <Container-id> <Command>
    OR:-
    docker exec -it <Container-id> <Command>
- -it  :  "can be written as -i -t"
- -i: to connect terminal with container STDIN
- -t: nice format of output
___
### 8- Run Terminal inside Docker container:
    docker exec -it <Container-id> sh
- to exit container Terminal:
            
      press "command+d"
      OR:-
      exit
___
### 9- Start Docker container with Terminal:
    docker run -it <image-name> sh
___
### 10- Start Docker container with Port Mapping:
    docker run -p <incoming/Port> : <Port/inside> <image-id>
___

# Building Custom Images Through Docker Server

- [Create Custom Docker image](#1--Create-Custom-Docker-image)
- [Tagging a Custom Image](#2--Tagging-a-Custom-Image)
___
### 1- Create Custom Docker image:

1. Specify base image
2. Run some commands to install additional programs
3. Specify a command to run on container startup
    
        touch Dockerfile 

- follow  [example](https://github.com/Ahmedhemaz/DockerCheatSheet/blob/master/docker/custom-docker-image-ex/Dockerfile) 
- after creating the Dockerfile run 
    
      docker build .
- make sure that you are in the same Dockerfile directory 
- then take the container id and start it with

      docker run <image-id>

##### *Note that when building docker image after each Dockerfile command will create intermediate container with the created image file system snapshot till reach the last command and generate the last docker image

##### *Note that when building docker image again will use cached images unless you added some new commands will fetch images from docker hub starting from that line downwords
___
### 2- Tagging a Custom Image:
    docker build -t yourDockerUserName/ProjectName:latest .
___
# Building  multiple containers with "Docker-compose":
- [Usage](#1--Usage)
- [docker-compose file structure](#2--docker-compose-file-structure)
- [docker-compose commands](#3--docker-compose-commands)


### 1- Usage:
- to use multiple containers and set a network infrastructure between contaiers 
___
### 2- docker-compose file structure:
- follow [example](https://github.com/Ahmedhemaz/DockerCheatSheet/blob/master/docker/docker-compose-example/docker-compose.yml) 
___
#### 2-1 restart policies:
- "no" : Never attempt to restart this container if it stops or crashes
- always : If this container stops for any reason always attempt to restart
- on-failure : Only restart this container with an error code
- unless-stopped : Always restart unless (Developer) forcibly stop it 
___
## 3- docker-compose commands:
- [run containers in docker-compose file](#3-1-run-containers-in-docker-compose-file)
- [run containers in background](#3-2-run-containers-in-background)
- [stop all running containers](#3-3-stop-all-running-containers)
- [list all running containers](#3-4-list-all-running-containers)
___
### 3-1 run containers in docker-compose file:
      docker-compose up
- docker compose will make default network between containers 
- if you are using database or some service you can connect with them by providing the name of service in the host part of your application and docker compose will connect them 

#### *Note: if you wanna rebuild an image you can use 
      docker-compose up --build
___
### 3-2 run containers in background:
      docker-compose up -d
___
### 3-3 stop all running containers:
      docker-compose down
___
### 3-4 list all running containers:
      docker-compose ps
- should run it from docker-compose file location
___
