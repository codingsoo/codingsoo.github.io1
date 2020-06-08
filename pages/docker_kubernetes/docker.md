---
title: Docker
keywords: docker
last_updated: June 8, 2020
tags: [docker]
summary: "Let's start Docker!"
sidebar: home_sidebar
permalink: docker.html
folder: kubernetes
---

## Docker

### Introduction

Docker is an open platform for developing, shipping, and running applications using LXC (Linux Containers). 

![docker-architecture](images/kubernetes/docker-architecture.svg "https://docs.docker.com/get-started/overview/")

You can pull and build images, and run them using LXC. 
There are lots of pre-built images in DockerHub.
You can also upload your image to DockerHub privately or publically.
You can manage this process through Docker client.

### What is the Docker image?

Docker image is a pre-built read-only environment which can run on the Docker platform as a container.
You can use pre-built images from DockerHub or build your own images.
The usual process is

1. Build your own image based on other pre-built images using Dockerfile.
2. Run your application in containers using your image.
3. Before important update, commit the changes to a Docker image.
4. If update failed, rollback using the committed Docker image.


![docker-image-layer](images/kubernetes/docker-image-layer.jpg "https://stackoverflow.com/questions/55174274/understanding-docker-layers-and-future-changes")

Docker image has layered architecture to romove duplications. For example, if image A and image B have common part, we can build the common part once and use it separately instead of building the common part separately. You can check the layer information using "docker inspect" command. The layers are stored in the overlay2 directory.

### Dockerfile

- A Dockerfile is a text file which contains a series of commands or instructions. 
- These instructions are executed in the order in which they are written.
- Execution of these instructions takes place on a base image. 
- On building the Dockerfile, the successive actions form a new image from the base parent image.

   - [Lab #1: Installing GIT](https://dockerlabs.collabnix.com/beginners/dockerfile/lab1_dockerfile_git.html)
   - [Lab #2: ADD instruction](https://dockerlabs.collabnix.com/beginners/dockerfile/Lab-2-Create-an-image-with-ADD-instruction.html)
   - [Lab #3: COPY instruction](https://dockerlabs.collabnix.com//beginners/dockerfile/lab4_dockerfile_copy.html)
   - [Lab #4: CMD instruction](https://dockerlabs.collabnix.com//beginners/dockerfile/lab4_cmd.html)
   - [Lab #5: ENTRYPOINT instruction](https://dockerlabs.collabnix.com/beginners/dockerfile/Dockerfile-ENTRYPOINT.html)
   - [Lab #6: WORKDIR instruction](https://dockerlabs.collabnix.com/beginners/dockerfile/WORKDIR_instruction.html)
   - [Lab #7: RUN instruction](https://dockerlabs.collabnix.com/beginners/dockerfile/Lab-7-Create-an-image-with-EXPOSE-instruction.html)
   - [Lab #8: ARG instruction](https://dockerlabs.collabnix.com//beginners/dockerfile/arg.html)
   - [Lab #9: EXPOSE instruction](https://dockerlabs.collabnix.com/beginners/dockerfile/Lab-7-Create-an-image-with-EXPOSE-instruction.html)
   - [Lab #10: VOLUME instruction](https://dockerlabs.collabnix.com/beginners/dockerfile/Lab%2310:VOLUME_instruction.html)
   - [Lab #11: EXPOSE instruction](https://dockerlabs.collabnix.com/beginners/dockerfile/Lab%2311:EXPOSE_instruction.html)
   - [Lab #12: LABEL instruction](https://dockerlabs.collabnix.com/beginners/dockerfile/Label_instruction.html)
   - [Lab #13: ONBUILD instruction](https://dockerlabs.collabnix.com/beginners/dockerfile/onbuild.html)
   - [Lab #14: HEALTHCHECK instruction](https://dockerlabs.collabnix.com/beginners/dockerfile/healthcheck.html)
   - [Lab #15: SHELL instruction](https://dockerlabs.collabnix.com/beginners/dockerfile/Lab-14-Create-an-image-with-SHELL-instruction.html)
   - [Lab #16: Entrypoint Vs RUN](https://dockerlabs.collabnix.com/beginners/dockerfile/entrypoint-vs-run.html)
   - [Lab #17: USER instruction](https://dockerlabs.collabnix.com/beginners/dockerfile/user.html)
   - [Writing Dockerfile with Hello Python Script Added](https://dockerlabs.collabnix.com/beginners/dockerfile/lab_dockerfile_python.html)

The soure in this section is from https://dockerlabs.collabnix.com/

### Private Registry

Instead of using DockerHub, you can use private registry. DockerHub has an image for the private registry server.

```
docker run -d --name docker-registry -p 5000:5000 registry
sudo docker tag xxx 127.0.0.1:5000/xxx
sudo docker push 127.0.0.1:5000/xxx
```

If you need authentication information, visit https://docs.docker.com/registry/configuration/#auth / https://github.com/collabnix/dockerlabs/blob/9f8999b55efcbd2c1ddbba2aa7eab03d7b56e21e/intermediate/registry/part-3.md

### Cheatsheet

```
# Run = create + exec
# Run a container with port linking. If you don't have the image, Docker automatically search it from DockerHub
docker run -p 8080:8080 --name [container name] [image name:version]

# Run a container and access bash
docker run -it [image name] /bin/bash

# Run a container in background
docker run -d [image name]

# Run a container with environment variable
docker run -e PASSWORD=0000 [image name]

# Run a container with removing option. The container is deleted when it stops.
docker run --rm [image name]

# Run a container with volume mounting and local file sharing
docker run -v [host path]:[container path]:[permission -> default:ro]]

# See logs of the container
docker logs [container name]

# Inspect a container or an image
docker inspect [container name | image name]

# Delete all images
sudo docker rmi `sudo docker images -q`

# Stop all containers
sudo docker stop `sudo docker ps -a -q`

# Delete all containers
sudo docker rm -f `sudo docker ps -a -q`

# Change the image name
sudo docker tag [previous name] [new name]

# Push the image to DockerHub (image name should be username/imagename format)
sudo docker login
sudo docker tag xxx:version user_name/xxx:version
sudo docker push [image name]

# Check image history
sudo docker history [image name]

# Make an image using container
sudo docker commit [container name] [image name]
```

### Further Studying Materials

1. https://dockerlabs.collabnix.com/
2. https://docs.docker.com/get-started/overview/
