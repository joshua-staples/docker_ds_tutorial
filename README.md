## Pre-requisits:

- MacOS, Linux, Windows
- Docker Desktop

Check install:

```
docker ps 
```
```
docker version
```
```
docker run hello-world
```
To show all running containers:
```
docker ps -a
```
One last example:
```
docker run docker/whalesay cowsay Hello there!
```
If the docker image doesn't exist locally, then docker will automatically pull it from [dockerhub](https://hub.docker.com/)

[Here](https://hub.docker.com/r/docker/whalesay) are some more details on whalesay.

## Baisc Workflow

Build, run, push, pull

__Build__

Every docker image we used above was built by someone. The build command is used to build your own custom image based on a Dockerfile. 

To see all of the images you have downloaded use this command:
```
docker images
```

https://medium.com/@deepakshakya/beginners-guide-to-use-docker-build-run-push-and-pull-4a132c094d75

## Image

https://hub.docker.com/r/jupyter/all-spark-notebook

## Container


