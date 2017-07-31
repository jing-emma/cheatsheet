### docker terminology
1. __image__: executable package that includes everything to run a piece of software
2. __container__:a runtime instance of an image
3. __service__: container in production.  A docker-compose.yml file is a YAML file that defines how Docker containers should behave in production. for example, how many container do you want to run, how do you scale your app, load balancing etc.

## docker image
### Show all images on this machine
docker images ls      

### Remove the specified image from this machine
docker image rm <imagename>    

### Log in this CLI session using your Docker credentials
docker login    

### Tag <image> for upload to registry
docker tag <image> username/repository:tag  

### Upload tagged image to registry
docker push username/repository:tag  

## docker run
### Run image from a registry
docker run username/repository:tag  

### Exec bash inside a running container
docker exec -it CONTAINER_ID bash

### Create image named friendlyname using this directory's Dockerfile
docker build -t friendlyname .

### Run "friendlyname" mapping port 4000 to 80
docker run -p 4000:80 friendlyname

### Same thing, but in detached mode
docker run -d -p 4000:80 friendlyname 

### See a list of all running containers
docker ps 

### Gracefully stop the specified container
docker stop <hash>    

### See a list of all containers, even the ones not running
docker ps -a           

### Force shutdown of the specified container
docker kill <hash>     

### Remove the specified container from this machine
docker rm <hash>   

### Remove all containers from this machine
docker rm $(docker ps -a -q)           
                          


