# Docker/Podman Cheat Sheet

Below is a list of sample docker commands to help you through some of the labs

## Listing Docker Resources

`docker ps` - lists all the running containers

`docker ps -a` - lists all the running and exited containers

`docker images` - lists all the images

`docker volume ls` - lists all the volumes

`docker network ls` - lists all the networks


## Run a command in a new container:

`docker run [IMAGE] [COMMAND]`

`docker run --rm [IMAGE]` – removes a container after it exits.

`docker run -td [IMAGE]` – starts a container and keeps it running.

`docker run -it [IMAGE]` – starts a container, allocates a pseudo-TTY connected to the container’s stdin, and creates an interactive bash shell in the container.

`docker run -it-rm [IMAGE]` – creates, starts, and runs a command inside the container. Once it executes the command, the container is removed.


## Starting and Stopping Containers

`docker start [CONTAINER]` - Start a container

`docker stop [CONTAINER]` - Stop a running container

`docker restart [CONTAINER]` - Stop a running container and start it up again

`docker rm [CONTAINER]` - Delete a container (if it is not running)

`docker kill [CONTAINER]` - Kill a container by sending a SIGKILL to a running container

## Docker Image Commands

`docker build [URL]` - Create an image from a Dockerfile

`docker build -t `– builds an image from a Dockerfile in the current directory and tags the image

`docker pull [IMAGE]` - Pull an image from a registry

`docker push [IMAGE]` - Push an image to a registry

`docker rmi [IMAGE]` - Remove an image

`docker load [TAR_FILE/STDIN_FILE]` - Load an image from a tar archive or stdin

`docker save [IMAGE] > [TAR_FILE]` - Save an image to a tar archive, streamed to STDOUT with all parent layers, tags, and versions

## Debugging containers

`docker logs [CONTAINER]` - List the logs from a running container

`docker inspect [OBJECT_NAME/ID]` - List low-level information on Docker objects

`docker events [CONTAINER]` - List real-time events from a container

`docker top [CONTAINER]` - Show running processes in a container
