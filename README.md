# docker-cheatsheet
### This document contains some common questions and their answers about docker
---
### 1- Show docker version and exposed ports for a specific image
* show docker version:

 Syntax:
 
    docker image inspect [IMAGE] -f '{{ .DockerVersion }}'
    
* Show exposed ports:

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
### 5-
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
  

     
