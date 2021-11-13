# Docker Compose

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration. To learn more about all the features of Compose, see the [list of features](https://docs.docker.com/compose/overview/#features).

> To see one of my example `docker-compose.yml` files, go [here](docker-compose.yml).


```sh
$ docker-compose up
# same as docker run <image name>
```

This allows us to create and start multiple images at the same time. 

Docker compose will read you configuration file `docker-compose.yml` and create and start the containers based on your configuration.

```sh
$ docker-compose up -d
```

* It launches all containers in the background and free's up out terminal


```sh
$ docker-compose down
# same as docker stop <container ID>
```

This allows us to (at the same time) stop all created containers made by docker-compose from our `docker-compose.yml` file.


## Docker compose build

```sh
$ docker-compose up --build
# same as docker build .
# and docker run <image name>
```

This allows us to rebuild all of our containers and start thema at the same time.

Again, docker compose will read you configuration file `docker-compose.yml` and create and start the containers based on your configuration.

```sh
$ docker-compose ps
# same as docker ps but only for composed containers
```