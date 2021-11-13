# Image commands

Images are just [templates for docker containers](https://docs.docker.com/engine/understanding-docker/#how-does-a-docker-image-work).



## Load/Save image

Load an image from file:

```sh
$ docker load < my_image.tar.gz
```

Save an existing image:

```sh
$ docker save my_image:my_tag | gzip > my_image.tar.gz
```

## Import/Export container

Import a container as an image from file:

```sh
$ cat my_container.tar.gz | docker import - my_image:my_tag
```

Export an existing container:

```sh
$ docker export my_container | gzip > my_container.tar.gz
```

## Difference between loading a saved image and importing an exported container as an image

Loading an image using the `load` command creates a new image including its history.  
Importing a container as an image using the `import` command creates a new image excluding the history which results in a smaller image size compared to loading an image.