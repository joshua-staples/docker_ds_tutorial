## Prerequisites:

- MacOS, Linux, Windows
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (once installed it can run all of our commands, or we can use the CLI)

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
To show all running containers (the -a here is a tag meaning 'all'):
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

Build, run, push, pull.

### Build

Every docker image we used above was built by someone. The build command is used to build your own custom image based on a Dockerfile. Building your own image is not difficult, but it is an advanced topic that will not be covered in this tutorial, we will be using pre-built images. 

You can see all of the images you have downloaded locally using this command:
```
docker images
```

### Run

We've already used the ```docker run``` command. This command runs the image specified. An image can either run a specified file it contains (a deployed app, like the examples above) or it can open a web-server for development, which is what we will be doing. 

### Push

If you want to make your own dockerhub account you can push any images your make using the ```docker push image_name``` command. (this is beyond the scope of this tutorial.)

### Pull

The ```docker pull image_name``` command allows you to pull any prebuilt image from dockerhub. 

This is useful if you already know the language your project will be in, as you can then just pull an image that contains that language. Popular images can be found by browsing [dockerhub](https://hub.docker.com/). 

[Additional Reading](https://medium.com/@deepakshakya/beginners-guide-to-use-docker-build-run-push-and-pull-4a132c094d75)

## Image

https://hub.docker.com/r/jupyter/all-spark-notebook

## Container

## Sharing Work

You can either ```docker save image_name``` an image or ```docker export container_name``` a container. This will output a tar (compressed) file to standard output, you can save this to a .tar file by using ```'container_name' > dk.container_name.latest.tar```. Then you can use ```docker load file``` or ```docker import file``` on a different machine.
