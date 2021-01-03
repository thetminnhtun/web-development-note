# Docker Commands

### Download image

```sh
$ docker pull [IMAGE]
```

eg.

```sh
$ docker pull ubuntu
```

### Show all images

```sh
$ docker images
```

### Remove image

```sh
$ docker images rm [IMAGE]
```

### Remove all images

```sh
$ docker rmi $(docker images -a -q)
```
