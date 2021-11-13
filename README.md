# Docker Primer

Primer for getting started with Docker. Primer is written primarily for linux/mac, and provides some of the most common commands required to get your Docker set-up going. 

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com) 

To contribute, click [here](CONTRIBUTING.md).

## Features
 - Docker basics
 - Most common commands
 - Examples
 - Links to videos
 - Links to blog posts

## Table of Contents

* [What is Docker?](#what-is-docker)
* [Why use Docker?](#why-use-docker)
* [Docker Architecture](#docker-architecture)
* [Installation requirements](#instalation-requirements)
* [Installation](#installation)
* [Using Docker](#using-docker)
* [Most common Docker commands](#most-common-docker-commands)
* [Container commands](#container-commands)
* [Image commands](#image-commands)
* [Network commands](#network-commands)
* [Volumes commands](#volumes-commands)
* [Registry commands](#registry-commands)
* [Dockerfile](#dockerfile)
* [Layers](#layers)
* [Links](#links)
* [Exposing Ports](#exposing-ports)
* [Security](#security)
* [Best Practices](#best-practices)
* [Docker-Compose](#docker-compose)

## What is Docker?

[Docker](https://docs.docker.com/get-started/overview/) is an open platform for developing, shipping, and running applications.

## Why use Docker?

Docker allows developers to work in standardized environments using [containers](https://docs.docker.com/get-started/overview/#docker-objects). What this essentially means is that "“Dockerized” apps are completely portable and can run anywhere, on any system, without the need to configure and set-up your enviroment.

## Docker Architecture

Docker uses a [client-server architecture](https://docs.docker.com/get-started/overview/#docker-architecture). The Docker *client* (aka. Docker CLI) talks to the Docker *daemon*, which does the heavy lifting of building, running, and distributing your Docker containers.

![Edit This](docs/images/docker-architecture.svg)

### Docker client

The Docker *client* (`docker`) is the primary way to interact with Docker. When you use commands such as `docker run`, the client sends these commands to the docker *daemon* (`dockerd`), which carries them out. 

### Docker daemon

The Docker *daemon* (`dockerd`) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

### Docker registry

A Docker *registry* stores Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can even run your own private registry.

## Instalation requirements

### Linux

The 3.10.x kernel is [the minimum requirement](https://docs.docker.com/engine/installation/binaries/#check-kernel-dependencies) for Docker.

### MacOS

10.8 “Mountain Lion” or newer is required.

### Windows 10

Hyper-V must be enabled in BIOS

VT-D must also be enabled if available (Intel Processors). 

## Installation

If you are a complete Docker newbie, you should probably follow the [tutorial](https://docs.docker.com/engine/getstarted/) for your operating system.

### Linux

Run this quick and easy install script provided by Docker:

```sh
$ curl -sSL https://get.docker.com/ | sh
```

If you don't want to run a random shell script, please see the [installation](https://docs.docker.com/engine/installation/linux/) instructions for your distribution.

### macOS

If you have Homebrew-Cask, type in your terminal:

```sh
$ brew cask install docker
```

Alternativley, you can download and install [Docker Community Edition](https://www.docker.com/community-edition). 

Once you've installed Docker Community Edition, click the docker icon in Launchpad. Then start up a container by typing:

```sh
$ docker run hello-world
```

That's it, you now have a running Docker container.

### Windows 10

Official instructions to install Docker Desktop for Windows can be found [here](https://hub.docker.com/editions/community/docker-ce-desktop-windows).

> If you're using windows, please check out a more detailed explanation I've written for you [here](docs/examples/windows.md).

Once installed, open powershell as administrator and run:

```sh
# Display the version of docker installed:
$ docker version

# Pull, create, and run 'hello-world' container:
$ docker run hello-world
```

That's it, you now have a running Docker container.

## Using Docker 

### Check Version

It is very important that you always know the current version of Docker you are currently running on at any point in time.

* [`docker version`](https://docs.docker.com/engine/reference/commandline/version/) shows which version of docker you have running.

Get detailed information about your version (client and server) by running:

```sh
$ docker version
# Output will be detailed information about your docker version
```

Get only the version:

```sh
$ docker version --format '{{.Server.Version}}'
# 1.8.0
```

## Most common Docker commands

These are some of the most common commands while using Docker. All of them link to Docker documentation page where you can see examples of usage.

> I have also made a folder with all of my saved commands and examples. Check it out [here](docs/examples).

## Container commands

A [Container](https://docs.docker.com/get-started/overview/#docker-objects) is a runnable instance of an image. And an [image](https://docs.docker.com/get-started/overview/#docker-objects) is a read-only template with instructions for creating a Docker container.

> To see some of my own container related examples and saved commands, go [here](docs/examples/commands_container.md).

### Lifecycle

* [`docker create`](https://docs.docker.com/engine/reference/commandline/create) creates a container but does not start it.
* [`docker rename`](https://docs.docker.com/engine/reference/commandline/rename/) allows the container to be renamed.
* [`docker run`](https://docs.docker.com/engine/reference/commandline/run) creates and starts a container in one operation.
* [`docker rm`](https://docs.docker.com/engine/reference/commandline/rm) deletes a container.
* [`docker update`](https://docs.docker.com/engine/reference/commandline/update/) updates a container's resource limits.



### Starting and Stopping

* [`docker start`](https://docs.docker.com/engine/reference/commandline/start) starts a container so it is running.
* [`docker stop`](https://docs.docker.com/engine/reference/commandline/stop) gracefully stops a running container.
* [`docker restart`](https://docs.docker.com/engine/reference/commandline/restart) stops and starts a container.
* [`docker pause`](https://docs.docker.com/engine/reference/commandline/pause/) pauses a running container, "freezing" it in place.
* [`docker unpause`](https://docs.docker.com/engine/reference/commandline/unpause/) will unpause a running container.
* [`docker wait`](https://docs.docker.com/engine/reference/commandline/wait) blocks until running container stops.
* [`docker kill`](https://docs.docker.com/engine/reference/commandline/kill) sends a SIGKILL to a running container.
* [`docker attach`](https://docs.docker.com/engine/reference/commandline/attach) will connect to a running container.


### Info

* [`docker ps`](https://docs.docker.com/engine/reference/commandline/ps) shows running containers.
* [`docker logs`](https://docs.docker.com/engine/reference/commandline/logs) gets logs from container.
* [`docker inspect`](https://docs.docker.com/engine/reference/commandline/inspect) looks at all the info on a container (including IP address).
* [`docker events`](https://docs.docker.com/engine/reference/commandline/events) gets events from container.
* [`docker port`](https://docs.docker.com/engine/reference/commandline/port) shows public facing port of container.
* [`docker top`](https://docs.docker.com/engine/reference/commandline/top) shows running processes in container.
* [`docker stats`](https://docs.docker.com/engine/reference/commandline/stats) shows containers' resource usage statistics.
* [`docker diff`](https://docs.docker.com/engine/reference/commandline/diff) shows changed files in the container's FS.

### Import / Export

* [`docker cp`](https://docs.docker.com/engine/reference/commandline/cp) copies files or folders between a container and the local filesystem.
* [`docker export`](https://docs.docker.com/engine/reference/commandline/export) turns container filesystem into tarball archive stream to STDOUT.

### Executing Commands

* [`docker exec`](https://docs.docker.com/engine/reference/commandline/exec) to execute a command inside the container.

### Data management

* [`docker system df`](https://docs.docker.com/engine/reference/commandline/system_df/) shows Docker disk usage (for all Docker objects)
* [`docker system prune`](https://docs.docker.com/engine/reference/commandline/system_prune/) will delete ALL unused data (images, containers, networks, volumes)
* [`docker volume prune`](https://docs.docker.com/engine/reference/commandline/volume_prune/) will delete all unused volumes 
* [`docker network prune`](https://docs.docker.com/engine/reference/commandline/network_prune/) will delete all unused networks
* [`docker container prune`](https://docs.docker.com/engine/reference/commandline/container_prune/) will delete all unused containers
* [`docker image prune`](https://docs.docker.com/engine/reference/commandline/image_prune/) will delete all unused images

## Image commands

Images are just [templates for docker containers](https://docs.docker.com/engine/understanding-docker/#how-does-a-docker-image-work).

> To see some of my own image related examples and saved commands, go [here](docs/examples/commands_image.md).

### Lifecycle

* [`docker images`](https://docs.docker.com/engine/reference/commandline/images) shows all images.
* [`docker import`](https://docs.docker.com/engine/reference/commandline/import) creates an image from a tarball.
* [`docker build`](https://docs.docker.com/engine/reference/commandline/build) creates image from Dockerfile.
* [`docker commit`](https://docs.docker.com/engine/reference/commandline/commit) creates image from a container, pausing it temporarily if it is running.
* [`docker rmi`](https://docs.docker.com/engine/reference/commandline/rmi) removes an image.
* [`docker load`](https://docs.docker.com/engine/reference/commandline/load) loads an image from a tar archive as STDIN, including images and tags (as of 0.7).
* [`docker save`](https://docs.docker.com/engine/reference/commandline/save) saves an image to a tar archive stream to STDOUT with all parent layers, tags & versions (as of 0.7).

### Info

* [`docker history`](https://docs.docker.com/engine/reference/commandline/history) shows history of image.
* [`docker tag`](https://docs.docker.com/engine/reference/commandline/tag) tags an image to a name (local or registry).

## Network commands

Docker has a [networks](https://docs.docker.com/engine/userguide/networking/) feature that automatically creates 3 network interfaces when you create a container (bridge, host, none).

> To read a bit more about it and see some of my own examples and saved commands, go [here](docs/examples/commands_network.md).


### Lifecycle

* [`docker network create`](https://docs.docker.com/engine/reference/commandline/network_create/) Create a new network (default type: bridge).
* [`docker network rm`](https://docs.docker.com/engine/reference/commandline/network_rm/) Remove one or more networks by name or identifier. No containers can be connected to the network when deleting it.

### Info

* [`docker network ls`](https://docs.docker.com/engine/reference/commandline/network_ls/) List networks
* [`docker network inspect`](https://docs.docker.com/engine/reference/commandline/network_inspect/) Display detailed information on one or more networks.

### Connection

* [`docker network connect`](https://docs.docker.com/engine/reference/commandline/network_connect/) Connect a container to a network
* [`docker network disconnect`](https://docs.docker.com/engine/reference/commandline/network_disconnect/) Disconnect a container from a network


## Volumes commands

Docker [volumes](https://docs.docker.com/engine/tutorials/dockervolumes/) are are files and folders that can be attached to containers (or perserved from within the container).

> To read a bit more about it and see some of my own volumes related examples and saved commands, go [here](docs/examples/commands_volumes.md).

### Lifecycle

* [`docker volume create`](https://docs.docker.com/engine/reference/commandline/volume_create/)
* [`docker volume rm`](https://docs.docker.com/engine/reference/commandline/volume_rm/)

### Info

* [`docker volume ls`](https://docs.docker.com/engine/reference/commandline/volume_ls/)
* [`docker volume inspect`](https://docs.docker.com/engine/reference/commandline/volume_inspect/)


## Registry commands

A repository is a *hosted* collection of tagged images that together create the file system for a container.

A registry is a *host* -- a server that stores repositories and provides an HTTP API for [managing the uploading and downloading of repositories](https://docs.docker.com/engine/tutorials/dockerrepos/).

Docker.com hosts its own [index](https://hub.docker.com/) to a central registry which contains a large number of repositories.  Having said that, the central docker registry [does not do a good job of verifying images](https://titanous.com/posts/docker-insecurity) and should be avoided if you're worried about security.

* [`docker login`](https://docs.docker.com/engine/reference/commandline/login) to login to a registry.
* [`docker logout`](https://docs.docker.com/engine/reference/commandline/logout) to logout from a registry.
* [`docker search`](https://docs.docker.com/engine/reference/commandline/search) searches registry for image.
* [`docker pull`](https://docs.docker.com/engine/reference/commandline/pull) pulls an image from registry to local machine.
* [`docker push`](https://docs.docker.com/engine/reference/commandline/push) pushes an image to the registry from local machine.


## Dockerfile

[The configuration file](https://docs.docker.com/engine/reference/builder/). Sets up a Docker container when you run `docker build` on it. Vastly preferable to `docker commit`.  

### Dockerfile commands

* [.dockerignore](https://docs.docker.com/engine/reference/builder/#dockerignore-file) defines which files and folders should be avoided while building a docker image.
* [FROM](https://docs.docker.com/engine/reference/builder/#from) sets the Base Image for subsequent instructions.
* [RUN](https://docs.docker.com/engine/reference/builder/#run) execute any commands in a new layer on top of the current image and commit the results.
* [CMD](https://docs.docker.com/engine/reference/builder/#cmd) provide defaults for an executing container.
* [EXPOSE](https://docs.docker.com/engine/reference/builder/#expose) informs Docker that the container listens on the specified network ports at runtime.  NOTE: does not actually make ports accessible.
* [ENV](https://docs.docker.com/engine/reference/builder/#env) sets environment variable.
* [ADD](https://docs.docker.com/engine/reference/builder/#add) copies new files, directories or remote file to container.  Invalidates caches. Avoid `ADD` and use `COPY` instead.
* [COPY](https://docs.docker.com/engine/reference/builder/#copy) copies new files or directories to container.  By default this copies as root regardless of the USER/WORKDIR settings.  Use `--chown=<user>:<group>` to give ownership to another user/group.  (Same for `ADD`.)
* [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#entrypoint) configures a container that will run as an executable.
* [VOLUME](https://docs.docker.com/engine/reference/builder/#volume) creates a mount point for externally mounted volumes or other containers.
* [USER](https://docs.docker.com/engine/reference/builder/#user) sets the user name for following RUN / CMD / ENTRYPOINT commands.
* [WORKDIR](https://docs.docker.com/engine/reference/builder/#workdir) sets the working directory.
* [ARG](https://docs.docker.com/engine/reference/builder/#arg) defines a build-time variable.
* [ONBUILD](https://docs.docker.com/engine/reference/builder/#onbuild) adds a trigger instruction when the image is used as the base for another build.
* [STOPSIGNAL](https://docs.docker.com/engine/reference/builder/#stopsignal) sets the system call signal that will be sent to the container to exit.
* [LABEL](https://docs.docker.com/config/labels-custom-metadata/) apply key/value metadata to your images, containers, or daemons.
* [SHELL](https://docs.docker.com/engine/reference/builder/#shell) override default shell is used by docker to run commands.
* [HEALTHCHECK](https://docs.docker.com/engine/reference/builder/#healthcheck) tells docker how to test a container to check that it is still working.

### Tutorial

* [Flux7's Dockerfile Tutorial](https://www.flux7.com/tutorial/docker-tutorial-series-part-3-automation-is-the-word-using-dockerfile/)

### Examples

* [Examples](https://docs.docker.com/engine/reference/builder/#dockerfile-examples)
* [Best practices for writing Dockerfiles](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)
* [Michael Crosby](http://crosbymichael.com/) has some more [Dockerfiles best practices](http://crosbymichael.com/dockerfile-best-practices.html) / [take 2](http://crosbymichael.com/dockerfile-best-practices-take-2.html).
* [Building Good Docker Images](http://jonathan.bergknoff.com/journal/building-good-docker-images) / [Building Better Docker Images](http://jonathan.bergknoff.com/journal/building-better-docker-images)
* [Managing Container Configuration with Metadata](https://speakerdeck.com/garethr/managing-container-configuration-with-metadata)
* [How to write excellent Dockerfiles](https://rock-it.pl/how-to-write-excellent-dockerfiles/)

## Layers

The versioned filesystem in Docker is based on layers. They're like [git commits or changesets for filesystems](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/).

## Links

Links are how Docker containers talk to each other [through TCP/IP ports](https://docs.docker.com/engine/userguide/networking/default_network/dockerlinks/).

> To read a bit more about it and see some of my own links related examples and saved commands, go [here](docs/examples/commands_links.md).

## Exposing ports

Exposing incoming ports through the host container is [fiddly but doable](https://docs.docker.com/engine/reference/run/#expose-incoming-ports).

> To read a bit more about it and see some of my own examples and saved commands, go [here](docs/examples/commands_ports.md).

## Security

The Docker [security](https://docs.docker.com/engine/security/security/) page goes into much more detail.

> To read a bit more about it and see some of my own (shorter) explanations, go [here](docs/examples/commands_security.md).

### Security Videos

* [Using Docker Safely](https://youtu.be/04LOuMgNj9U)
* [Securing your applications using Docker](https://youtu.be/KmxOXmPhZbk)
* [Container security: Do containers actually contain?](https://youtu.be/a9lE9Urr6AQ)
* [Linux Containers: Future or Fantasy?](https://www.youtube.com/watch?v=iN6QbszB1R8)


## Best Practices

This is where general Docker best practices and war stories go:

* [The Rabbit Hole of Using Docker in Automated Tests](http://gregoryszorc.com/blog/2014/10/16/the-rabbit-hole-of-using-docker-in-automated-tests/)
* [Bridget Kromhout](https://twitter.com/bridgetkromhout) has a useful blog post on [running Docker in production](http://sysadvent.blogspot.co.uk/2014/12/day-1-docker-in-production-reality-not.html) at Dramafever.
* There's also a best practices [blog post](http://developers.lyst.com/devops/2014/12/08/docker/) from Lyst.
* [Building a Development Environment With Docker](https://tersesystems.com/2013/11/20/building-a-development-environment-with-docker/)
* [Discourse in a Docker Container](https://samsaffron.com/archive/2013/11/07/discourse-in-a-docker-container)

## Docker-Compose

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration. To learn more about all the features of Compose, see the [list of features](https://docs.docker.com/compose/overview/#features).

> To see some of my own `docker-compose` examples and saved commands, go [here](docs/examples/docker_compose.md).

> To see one of my example `docker-compose.yml` files, go [here](docs/examples/docker-compose.yml).

## License

[MIT License](LICENCE)

## Inspiration for this primer
Many thanks to [Will Sargent](https://github.com/wsargent) for making his [docker cheet sheet](https://github.com/wsargent/docker-cheat-sheet). This primer is greatly inspired by his hard work. Please check out his repo and drop a star ;)