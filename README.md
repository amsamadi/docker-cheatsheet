# docker-cheatsheet
### This document contains some common questions and their answers about docker
---
### 1- Show docker version and exposed ports for a specific image
* show docker version:

 Syntax:
 
    docker image inspect [IMAGE] -f '{{ .DockerVersion }}'
    
* Show exposed ports

 Syntax:
  
    docker image inspect [IMAGE] -f '{{ .Config.ExposedPorts }}' 
  
---
### 2- How to save and load a docker images

* For save a image as a archive file

 Syntax:
 
    docker image save -o nginx.tar.gz nginx:1.20.0
    
* For load that image from archive file with different name to local image repository

 Syntax:
 
    docker image import nginx.tar.gz nginx:1.20.0-test
    
---
### 3- How to map a specific host port to a container

 Run:
      
    docker run -d --name nginx -p 8081:80 nginx:1.20.0
     
---
### 4- To verify which processes is running in container

 Syntax:
  
    docker container top nginx
---
### 5- What is docker proxy?
* The docker-proxy operates in userland, and simply receives any packets arriving at the host's specified port, that the kernel hasn't 'dropped' or forwarded, and redirects them to the container's port
---
### 6- What is a dangling image? 

* A dangling image is one that is not tagged and is not referenced by any container.
#### To remove dangling images:

 Syntax:
  
    docker image prune
---
### 7- What signal is sent to the container when the container is stopped by the Kill command?

* The docker kill subcommand kills one or more containers. The main process inside the container is sent SIGKILL signal

 Syntax:
  
    docker kill nginx
---
### 8- Install a nginx in apline container and create image from this container

 Run:
 
    docker run -dit --name alpine alpine
    docker exec -it alpine sh
       apk update && apk add nginx
       exit
    docker commit alpine alpine:nginx
---
### 9- When the container is paused, What happens to her process?
* The container stays running and uses memory but does not use the processor
---
### 10- Run the container from redis image and put the id of this container in the myredis.cid file

  Run:
  
    docker run -dit --name redis redis
    docker container inspect redis -f '{{ .Id }}' > myredis.cid
---
### 11- Run the container with the following specifications
* CPU=0.5 Core
* CPUS=0,2
* RAM=512 MB
* SWAP=256 MB  

  Run:
  
      docker run -d --name nginx --cpus 0.5 --cpuset-cpus 0,2 --memory 512m --memory-swap 768m nginx:1.20.0
---
### 12- Set environment variables for a docker container and show them in the output
* For example set CLASS=dws and NAME=soran
 
  Run:
  
      docker run -dit --name alpine -e CLASS=dws -e NAME=soran alpine
      docker exec alpine printenv
---
### 13- Mount Volume to a container
* For example mount /home/data in the host to the /data in the container and set it as a working directory

  Run:
  
      docker run -dit --name alpine -v /home/data/:/data -w /data alpine
---
### 14- What is Dockerfile
* A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image
---
### 15- What is the difference between docker container commit and docker build command
* The docker build command builds Docker images from a Dockerfile and a “context”. ... The build process can refer to any of the files in the context. For example, your build can use a COPY instruction to reference a file in the context

* Docker's commit command allows users to take a running container and save its current state as an image
---
### 15- What is the difference between ENV and ARG in dockerfile?
* ENV is mainly meant to provide default values for your future environment variables. Running dockerized applications can access environment variables. It’s a great way to pass configuration values to your project

* ARG values are not available after the image is built. A running container won’t have access to an ARG variable value
---
### 16- What is the difference between CMD and ENTRYPOINT in dockerfile?
* CMD sets default command and/or parameters, which can be overwritten from command line when docker container runs. ENTRYPOINT command and parameters will not be overwritten from command line unless you add the --entrypoint flag. Instead, all command line arguments will be added after ENTRYPOINT parameters
---
### 17- What is the difference between expose and publish ports?
* Exposing ports is a way of documenting which ports are used, but does not actually map or open any ports. Exposing ports is optional. You publish ports using the --publish or --publish-all flag to docker run . This tells Docker which ports to open on the container's network interface
---
### 18- What does it mean when we use the FROM in Dockerfile?
* 


###### [@dwsclass](https://github.com/dwsclass)dws-ops-004-docker
###### [@dwsclass](https://github.com/dwsclass)dws-ops-005-docker

     
