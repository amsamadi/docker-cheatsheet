# docker-cheatsheet
### This document contains some common questions and their answers about docker
---
## 1- Show docker version and exposed ports for a specific image
* show docker version:

 Syntax:
 
    docker image inspect [IMAGE] -f '{{ .DockerVersion }}'
    
* show exposed ports:

 Syntax:
 
    docker image inspect [IMAGE] -f '{{ .Config.ExposedPorts }}' 
  
---
## 2- how to save and load a docker images

#### Example
* for save a image as a archive file

 Syntax:
 
    docker image save -o nginx.tar.gz nginx:1.20.0
    
* for load that image from archive file with different name to local image repository

 Syntax:
 
    docker image import nginx.tar.gz nginx:1.20.0-test
    
---
## 3- how to map a specific host port to a container

 Syntax:
      
      docker run -d --name nginx -p 8081:80 nginx:1.20.0
     
---
## 4- for verify which processes is running in container

  Syntax:
  
      docker container top nginx
---
## 5-
---
## 6- What is a dangling image? 

#### A dangling image is one that is not tagged and is not referenced by any container.
#### To remove dangling images:

  Syntax:
  
      docker image prune
     
