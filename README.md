# Docker Commands Cheat Sheet

## Table of Contents
- [Basic Commands](#basic-commands)
- [Running Containers](#running-containers)
- [Building and Removing Images](#building-and-removing-images)
- [Managing Containers](#managing-containers)
- [Networking and Storage](#networking-and-storage)
- [Naming and Linking Containers](#naming-and-linking-containers)
- [Inspection and Execution](#inspection-and-execution)
- [Handling Permission Denied Error](#handling-permission-denied-error)
- [Docker Compose and Cleanup](#docker-compose-and-cleanup)

## Basic Commands
List running containers.
```
docker ps
```
List all containers, including stopped ones.
```
docker ps -a
```
List all images stored locally.
```
docker images
```
Download an image from Docker Hub.
```
docker pull <image>
```
Upload an image to Docker Hub.
```
docker push <user>/<image>
```

## Running Containers
Run a container in interactive mode.
```
docker run -it <image>
```
Run a container in detached mode (background).
```
docker run -d <image>
```
Run a container in detached mode without stopping.
```
docker run -t -d <image>
```

## Building and Removing Images
Build an image from a Dockerfile in the current directory.
```
docker build .
```
Build and name the image.
```
docker build -t <name> .
```
Remove an image.
```
docker rmi <image>
```
Remove all images.
```
docker rmi $(docker images -q)
```
Remove unused images.
```
docker image prune
```

## Managing Containers
Stop all containers.
```
docker stop $(docker ps -a -q)
```
Remove all containers.
```
docker rm $(docker ps -a -q)
```
Forcefully stop a container.
```
docker kill <container>
```
Force remove all containers.
```
docker rm $(docker ps -a -q) -f
```
Remove all stopped containers.
```
docker container prune -f
```

## Networking and Storage
Map a port for the container.
```
docker run -d -p <host-port>:<container-port> <image>
```
Mount a volume.
```
docker run -d -v <source>:<target> <image>
```

## Naming and Linking Containers
Run a container with a custom name.
```
docker run -d --name=<name> <image>
```
Rename an image.
```
docker tag <old-image>:<old-tag> <new-image>:<new-tag>
```
Rename a container.
```
docker rename <old-container> <new-container>
```
Link two containers.
```
docker run -d --link <container>:<alias> <image>
```

## Inspection and Execution
Get detailed information about an image or container.
```
docker inspect <image>
```
Set environment variables.
```
docker run -e <param>=<value> -d <image>
```
Attach to a running container.
```
docker attach <container>
```
Start a stopped container.
```
docker start <container>
```
Run a command inside a running container.
```
docker exec <container> <command>
```
Open a shell inside a container.
```
docker exec -it <container> /bin/bash
```

## Docker Compose and Cleanup
Restart a container.
```
docker restart <container>
```
Start services defined in `docker-compose.yml`.
```
docker compose up
```
Remove all unused containers, networks, images, and volumes.
```
docker system prune --volumes
```

---

## Handling Permission Denied Error

If you get a permission error when stopping a container:
```
docker stop <container-id>
```
Error:

```bash
Error response from daemon: cannot stop container: 57ebcb8a1411: permission denied
```

Run this command to resolve the issue:
```
sudo aa-remove-unknown
```
Then retry stopping the container:
```
docker stop <container-id>
```
