# Knowledge
## Binary Analysis
analysis binary without source code

## Cornucopia
generate binaries  
compiler optimizations  
feedback-guided learning
    
Data Base:  
unstripped (with debug symbols) binaries

## Docker
package up applications and preconfigured server environments  
file --build-> image --run-> container

### 2 ways for creating a docker image
Interactive:  
changing existing container environment and saving the resulting state as a new image

Dockerfile:  
specifications for creating a Docker image

### Image Layers
Form a image hierarchy, dependent on lower layers, layer changed most -> highest in the hierarchy

Container Layer (top):  
runtime layer that mark changes of containers from original images

Parent Image (bot):  
basic building blocks (first layer) for a container  
Typical parent image: stripped-down Linux distribution with DBMS or CMS

Base Image (bot):  
similar to parent image, but is empty and waiting for DIY

Manifest:  
JSON file comprises info for configuring container

### Container Registries:  
catalogs of storage locations (repositories) for container images  
Docker Hub, Red Hat Quay, Amazon ECR...

### Container Repositories:  
collection of multi versions for the same container image

# Requirments
## Docker
### Installation
[official step_by_step guid](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)

Manage Docker as a non-root user:
```
sudo groupadd docker
sudo usermod -aG docker $USER
```

### Create Docker Image
#### Interactive (1st way)
Create containner from original image, modify container, save changes to a new image

run container from image inside a shell:  
```docker run -it OLD_IMAGE_NAME:TAG bash```  
```OLD_IMAGE_NAME```: original image of the container  
```TAG```: specify image version (default the latest one)  
```–name```: specify container name (default random name)

configure container environment:  
```apt-get update && apt-get install PACKAGE_NAME```  
run inside the container shell

save container to image:  
```docker commit CONTAINER_NAME NEW_IMAGE_NAME```

#### Dockerfile (2nd way)
three-step process

example Dockerfile:  
```
# Use the official Ubuntu 18.04 as base
FROM ubuntu:18.04
# Install nginx and curl
RUN apt-get update &&\
apt-get upgrade -y &&\
apt-get install -y nginx curl &&\
rm -rf /var/lib/apt/lists/*
```  
```\```: backslash for line continuation

build image from Dockerfile:  
```docker build -t IMAGE_NAME:TAG Dockerfile_Directory```  
```-t```: set image name and tag

### Commands
list images:  
```docker images```

remove a image:  
```docker image rm IMAGE_NAME```

list all containers:  
```docker ps -a```

list active containers:  
```docker ps```

list stopped containers:  
```docker ps -a -f status=exited```

list all containers from a image:  
```docker ps -a -f ancestor=IMAGE_NAME```

remove a container:  
```docker rm CONTAINER_ID```