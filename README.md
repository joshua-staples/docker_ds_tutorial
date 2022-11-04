## What is Docker?

Docker is a way of running containers with specific coding packages/libraries pre-installed in them. Unlike a virtual environment which can have different packages from MacOS, to Windows, or Linux, Docker creates its own OS (usually linux) with all the packages installed, so that anyone, on any OS, can run your program or workspace. 

The major difference between a VM (vitual machine) and a Docker Container is that a container only runs one process, and once that process exits, the container exits. A VM can run many processes, as it is a virtual operating system. Because of this, a Docker container is very lightweight compared to a full VM.

## Prerequisites:

- MacOS, Linux, Windows
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (once installed it can run all of our commands, or we can use the CLI)
- WSL2 if on Windows

## Installation:

## Check Install:

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

## Basic Workflow

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

## All-Spark-Notebook Image

In our tutorial we will use the [all-spark-notebook image](https://hub.docker.com/r/jupyter/all-spark-notebook). This image contains Python, R, Spark, Jupyter, Pandas, and many other useful data-science libraries.  

1. Navigate to the directory you want to use your notebook in.
2. Run:
```docker run -it --rm -p 4040:4040 -p 8888:8888 -v "${PWD}":/home/jovyan/work jupyter/all-spark-notebook```

The -it instructs Docker to allocate a pseudo-TTY connected to the container’s stdin; creating an interactive bash shell in the container.
The --rm automatically remove the container when it exits.
The -p 4040:4040 -p 8888:8888 flag is telling docker to bind the port 4040 to your local machines port 4040 and the same for 8888. 4040 handles the server connection, while 8888 is the user interface of Jupyter.
The -v flag mounts the current working directory into the container. We are telling it to mount "${PWD}" (which gets our current directory) into the notebooks /home/jovyan/work directory. This allows the container to save the work being done in the container to a local directory as well.
If you close a server after working and then come back and start a new server your previous work should still be there because of the -v flag.

## Container

## Sharing Work

You can either use ```docker save image_name``` for an image or ```docker export container_name``` for a container. This will output a tar (compressed) file to standard output, you can save this to a .tar file by piping ```docker export container_name > dk.container_name.latest.tar```. Then you can use ```docker load file``` or ```docker import file``` on a different machine.
