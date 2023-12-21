Embarking on Docker? Don't miss ['Why we build Docker'](https://youtu.be/3N3n9FzebAA) by Solomon Hykes at dotScale conference 2013. Alternatively, explore ['Introduction to Docker'](https://youtu.be/Q5POuMHxW-0) by Solomon Hykes at Twitter University.

Explore Docker further by referring to the official [documentation](https://docs.docker.com/get-started/overview/)  
Install Docker using Docker Desktop for Windows and macOS, Docker Engine for Linux, and install [Portainer](https://docs.portainer.io/start/install-ce/server/docker/linux) if you prefer a graphical user interface (GUI).

The following commands are common across operating systems, but some may be specific to Linux

### Starting the Docker engine

First we need to start the engine (Docker Daemon), which listens to the API requests being made through the Docker client and manages Docker objects such as images, containers, networks, and volumes

```bash
sudo systemctl start docker
```

### Stopping the Docker engine

To completely stop the docker engine, we need to stop both docker and docker.socket ([unix socket](https://en.wikipedia.org/wiki/Unix_domain_socket) used by daemon to communicate with client)

```bash
sudo systemctl stop docker
sudo systemctl stop docker.socket
```

### Exploring Docker command

For options with docker, explore `man docker`  
For all available commands, explore `docker --help`

### Docker Run Command

Run command is used to create and run a new container from an image. If it fails to find that image locally, it pulls the image from the registry (Docker Hub is a public registry)  
usage: `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`

OPTIONS can be explored using the command `docker run --help`  
The popular options are `-i`, `-t`, `-d`(stands for interactive, tty and detach)

IMAGE can be a local image (use command `docker images`)  
or from registry (search using `docker search` or browser)

COMMAND that need to be executed after creating a container  
ARG Arguments for above command !

options, command and arguments are optional

```bash
docker run -i -t ubuntu
```

(If you are not able to run image without `sudo`, it means that there are no users in your docker user group. Create user by following [Linux Postinstall](https://docs.docker.com/engine/install/linux-postinstall) steps)

### Image Commands

An image is a read-only template with instructions for creating a Docker container. There are several commands to view, modify, create and delete images

**List Images**

```bash
docker images
```

usage: `docker images [OPTIONS] [REPOSITORY[:TAG]]`  
explore more options to list images using command `docker images --help`, one of them is to use `-q` option with images command to show only image IDs

**Pull Image**

```bash
docker pull ubuntu:22.04
```

usage: `docker pull [OPTIONS] NAME[:TAG|@DIGEST]`  
we can specify the particular tag of image to be downloaded from registry

**Remove Images**

```bash
docker rmi e4c58958181a 9c7a54a9a43c hello-world
```

usage: `docker rmi [OPTIONS] IMAGE [IMAGE...]`  
Remove one or more local images (with the image name or ID)

**Build Image**

```bash
docker build .
```

usage: `docker buildx build [OPTIONS] PATH | URL | -`  
Start building image from rules given in the Dockerfile, which can be local or remote (using url)

**Push Image**

usage: `docker push [OPTIONS] NAME[:TAG]`  
We can push our local image to remote registry using push command, we should first take care about the authentication to our registry (login for Docker Hub)

### Container Commands

A container is a runnable instance of an image. You can create, start, stop, move, or delete a container using the Docker API or CLI. You can also create a new image based on its current state.

**List Containers**

```bash
docker ps
```

usage: `docker ps [OPTIONS]`  
explore more options using `docker ps --help`, which contains `-a` option (used to show all the containers, the default is only running containers)

**Start or Stop Containers**

```bash
docker start 8640576ea339
docker stop 8640576ea339
```

usage: `docker start [OPTIONS] CONTAINER [CONTAINER...]`  
start or stop multiple containers using their names or IDs

**Remove Containers**

```bash
docker rm 8640576ea339
```

usage: `docker rm [OPTIONS] CONTAINER [CONTAINER...]`  
remove one or more containers

**Exec Command**

```bash
docker exec -it 8640576ea339 bash
```

usage: `docker exec [OPTIONS] CONTAINER COMMAND [ARG...]`  
execute commands in a running container, also we can provide options (which include interactive and other stuff)

**Commit Command**

```bash
docker commit 8640576ea339 new_image:0.01
```

usage: `docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]`  
we can create new image from the current container's state

**Other Commands**

There are some other commands like  
list of port mappings - `docker port CONTAINER`  
rename container - `docker rename CONTAINER NEW_VALUE`  
restart containers - `docker restart [options] CONTAINER [CONTAINER...]`  
fetch logs of a container - `docker logs [options] CONTAINER`

### Other Concepts

These are two other important topics to be covered,  
one is [Networking](https://docs.docker.com/network/) and the other is [Storage](https://docs.docker.com/storage/).  
Networking is very well explained by [NetworkChuck](https://youtu.be/bKFMS5C4CG0) !!