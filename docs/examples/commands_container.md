
# Container commands

A [Container](https://docs.docker.com/get-started/overview/#docker-objects) is a runnable instance of an image. And an [image](https://docs.docker.com/get-started/overview/#docker-objects) is a read-only template with instructions for creating a Docker container.

## Table of contents:
## Lifecycle

* [`docker create`](#docker-create)
* [`docker rename`](#docker-rename)
* [`docker run`](#docker-run)
* [`docker rm`](#docker-rm)



### docker create

```sh
$ docker create <image>
```

`docker create` command creates a container and prepares it for running. It **DOES NOT** start the container automatically.


### docker rename

```sh
$ docker rename <old_container_name> <new_container_name>
```

`docker rename` command allows us to rename an existing container.


### docker run

```sh
$ docker run <image_name/ID>
```

`docker run` command first creates a container, ant then starts that container.

```sh
$ docker run -d <image_name/ID>
```

This allows us to create and start a container, but it runs it in the background and allows us to use the terminal.


```sh
$ docker run -p 3000:3000 <image_name/ID>
```

This allows us to create and start a container and it maps ports 3000 (local) to 3000 (inside container). The ports don't have to match.


```sh
$ docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app <image id>
```

This is a complex command so I'll break it down:
* `-p 3000:3000` sets-up network ports mappings from local enviroment to the container
* `-v /app/node_modules` sets a docker volume for a node_modules folder **inside** the container. That means that that folder will not be changed with commands we run afterwards
* `-v $(pwd):/app` sets-up a docker volume for all files in the (local) working directory to the `/app` folder inside container.

This command is used when developing the app. It propagates all developmental changes to be immediatley visible inside the container.



### docker rm


```sh
$ docker rm <image_name/ID>
```

`docker rm` command removes the container that is referenced.

### docker build

```sh
$ docker build .
```

This allows us to build a new container in the current build context. Think of the build context as a folder from where this command is beeing issued.

To build the container, Docker will read your `Dockerfile` configuration (located in that folder).

### Building and tagging/naming the container 

```sh
$ docker build -t username/project_name:latest .
```

This allows us to tag (`-t`) our container and refer to it by this tag. This way you don't have to look for its ID every time you want to run a command on that container.

### Building a container from a custom file

```sh
$ docker build -f Dockerfile.dev .
```

* `-f` flag allows us to specify a file to build from

This allows us to build a docker image from file named differently than `Dockerfile`. In this case, the file is called `Dockerfile.dev` and it serves as a development Dockerfile


### docker exec

To enter a running container, attach a new shell process to a running container called foo, use: 

```sh
$ docker exec -it foo /bin/bash
```


### Get IP address

```sh
docker inspect $(dl) | grep -wm1 IPAddress | cut -d '"' -f 4
```

Or with [jq](https://stedolan.github.io/jq/) installed:

```sh
docker inspect $(dl) | jq -r '.[0].NetworkSettings.IPAddress'
```

Or using a [go template](https://docs.docker.com/engine/reference/commandline/inspect):

```sh
docker inspect -f '{{ .NetworkSettings.IPAddress }}' <container_name>
```

Or when building an image from Dockerfile, when you want to pass in a build argument:

```sh
DOCKER_HOST_IP=`ifconfig | grep -E "([0-9]{1,3}\.){3}[0-9]{1,3}" | grep -v 127.0.0.1 | awk '{ print $2 }' | cut -f2 -d: | head -n1`
echo DOCKER_HOST_IP = $DOCKER_HOST_IP
docker build \
  --build-arg ARTIFACTORY_ADDRESS=$DOCKER_HOST_IP 
  -t sometag \
  some-directory/
```

### Get port mapping

```sh
docker inspect -f '{{range $p, $conf := .NetworkSettings.Ports}} {{$p}} -> {{(index $conf 0).HostPort}} {{end}}' <containername>
```

### Find containers by regular expression

```sh
for i in $(docker ps -a | grep "REGEXP_PATTERN" | cut -f1 -d" "); do echo $i; done
```

### Get Environment Settings

```sh
docker run --rm ubuntu env
```

### Kill running containers

```sh
docker kill $(docker ps -q)
```

### Delete all containers (force!! running or stopped containers)

```sh
docker rm -f $(docker ps -qa)
```

### Delete old containers

```sh
docker ps -a | grep 'weeks ago' | awk '{print $1}' | xargs docker rm
```

### Delete stopped containers

```sh
docker rm -v $(docker ps -a -q -f status=exited)
```

### Delete containers after stopping

```sh
docker stop $(docker ps -aq) && docker rm -v $(docker ps -aq)
```

### Delete dangling images

```sh
docker rmi $(docker images -q -f dangling=true)
```

### Delete all images

```sh
docker rmi $(docker images -q)
```

### Delete dangling volumes

As of Docker 1.9:

```sh
docker volume rm $(docker volume ls -q -f dangling=true)
```

In 1.9.0, the filter `dangling=false` does _not_ work - it is ignored and will list all volumes.

### Show image dependencies

```sh
docker images -viz | dot -Tpng -o docker.png
```

### Slimming down Docker containers

- Cleaning APT in a `RUN` layer - This should be done in the same layer as other `apt` commands. Otherwise, the previous layers still persist the original information and your images will still be fat.
    ```Dockerfile
    RUN {apt commands} \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
    ```
- Flatten an image
    ```sh
    ID=$(docker run -d image-name /bin/bash)
    docker export $ID | docker import – flat-image-name
    ```
- For backup
    ```sh
    ID=$(docker run -d image-name /bin/bash)
    (docker export $ID | gzip -c > image.tgz)
    gzip -dc image.tgz | docker import - flat-image-name
    ```

### Monitor system resource utilization for running containers

To check the CPU, memory, and network I/O usage of a single container, you can use:

```sh
docker stats <container>
```

For all containers listed by ID:

```sh
docker stats $(docker ps -q)
```

For all containers listed by name:

```sh
docker stats $(docker ps --format '{{.Names}}')
```

For all containers listed by image:

```sh
docker ps -a -f ancestor=ubuntu
```

Remove all untagged images:

```sh
docker rmi $(docker images | grep “^” | awk '{split($0,a," "); print a[3]}')
```

Remove container by a regular expression:

```sh
docker ps -a | grep wildfly | awk '{print $1}' | xargs docker rm -f
```

Remove all exited containers:

```sh
docker rm -f $(docker ps -a | grep Exit | awk '{ print $1 }')
```


