# Knowledge
## Binary Analysis
analysis binary without source code

## Cornucopia
generate binaries  
compiler optimizations  
feedback-guided learning
    
    Data Base
        unstripped (with debug symbols) binaries

## Docker
package up applications and preconfigured server environments  
file --build-> image --run-> container

    Create a Docker image
        Interactive
            changing existing container environment and saving the resulting state as a new image 
        Dockerfile
            specifications for creating a Docker image

    Image Layers
        form a image hierarchy
        dependent on lower layers  
        layer changed most -> highest in the hierarchy

        Container Layer (top)
            runtime layer that mark changes of containers from original images

        Parent Image (bot)
            basic building blocks (first layer) for a container  
            Typical parent image: stripped-down Linux distribution with DBMS or CMS

        Base Image (bot)
            similar to parent image, but is empty and waiting for DIY

        Manifest
            JSON file comprises info for configuring container

    Container Registries
        catalogs of storage locations (repositories) for container images  
        Docker Hub, Red Hat Quay, Amazon ECR...

    ### Container Repositories
    collection of multi versions for the same container image

# Requirments
## Docker
### Installation
[official step_by_step guid](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)

### Manage Docker as a non-root user
```
sudo groupadd docker
sudo usermod -aG docker $USER
```

### Create Docker Image
Interactive

    run image in shell```docker run -it OLD_IMAGE_NAME:TAG bash```  

        OLD_IMAGE_NAME
            original image of the container
        
        TAG
            specify image version (default the latest one)  
        
        –name
            specify container name (default random name)

        local / Docker Hub (Download)

    configure container environment
    inside the container shell, run 
    ```
    apt-get update && apt-get install PACKAGE_NAME
    ```

    list active containers
    ```docker ps```

    save image
    ```docker commit CONTAINER_NAME NEW_IMAGE_NAME```