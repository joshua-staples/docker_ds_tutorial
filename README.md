## Prerequisites:

- MacOS, Linux, Windows
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (once installed it can run all of our commands, or we can use the CLI)
- WSL2 if on Windows
- VS Code

## Installation:

MacOS:
- Download [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- Go through the Docker Desktop installation process
- Open Docker Desktop and terminal
- Continue to Check Install

Windows:
- Open Powershell as admin
- Run ```wsl --install``` in powershell
- Install [Windows Terminal](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=en-us&gl=us)
- Open Windows Terminal
- Download [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- Go through the Docker Desktop installation process
- Open Docker Desktop
- Continue to Check Install (run commands in your Windows Terminal)

Linux:

- Run this command in the terminal:
```
sudo snap install docker 
```
- Continue to Check Install

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

## What is Docker?

Docker is a way of running containers with specific coding packages/libraries pre-installed in them. Unlike a virtual environment which can have different packages from MacOS, to Windows, or Linux, Docker creates its own OS (usually linux) with all the packages installed, so that anyone, on any OS, can run your program or workspace. 

The major difference between a VM (vitual machine) and a Docker Container is that a container only runs one process, and once that process exits, the container exits. A VM can run many processes, as it is a virtual operating system. Because of this, a Docker container is very lightweight compared to a full VM.

## Why Docker for Data Science

## Basic Workflow

Build, run, push, pull.

### Build

Every docker image we used above was built by someone. The build command is used to build your own custom image based on a Dockerfile. 

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
2. In a command prompt (or terminal) run ```docker pull jupyter/all-spark-notebook```
3. Run:
```docker run -it --rm -p 8888:8888 -v "${PWD}":/home/jovyan/work jupyter/all-spark-notebook``` (MacOS/Linux)
3. Run:
```docker run -it --rm -p 8888:8888 -v "$(pwd):/home/jovyan/work" jupyter/all-spark-notebook``` (Windows)

The ```-it``` flag instructs Docker to allocate a pseudo-TTY connected to the container’s stdin; creating an interactive bash shell in the container. I remeber this as 'integrated terminal'.

The ```--rm``` flag automatically removes the container when it exits.

The ```-p 8888:8888``` flag is telling docker to bind the port 8888 of the container to you local port 8888.

The ```-v``` flag mounts the current working directory into the container. We are telling it to mount ```"${PWD}"``` (which gets our current directory) into the notebooks ```/home/jovyan/work``` directory. This allows the container to save the work being done in the container to a local directory as well.

If you close a server after working and then come back and start a new server your previous work should still be there because of the -v flag.

All of this can also be done from the Docker Desktop app. You can also remove the --rm command if you do not want the container to be cleared after every run. 

## Building Our Own Image

- Open VS Code
- Open the folder you want to code in
- Create a ```requirements.txt``` file
  - In the file paste ```requests==2.27.1```
  - If unsure what version of libraries you are using, run the ```pip list``` command in your development environment.
- Create a python file ```main.py```
  - Paste the code:
```
import requests

r = requests.get('https://api.example.com/test')
r.status_code 
```
- Create a file named ```Dockerfile```
  - Paste the following in the Dockefile:
```
FROM python:3
ADD requirements.txt /
RUN pip install -r requirements.txt
ADD main.py /
CMD [ "python", "./main.py" ]
```

- Finally run this code:
```
docker build -t user_name/python-script:latest .
```

The ```-t``` flag allows for a name and optionally a tag in the 'name:tag' format.

The ```.``` at the end says to use the current directory to find all the files to build the image.

- You can test your new image by running:
```
docker run user_name/python-script:latest
```

## Container

If you have already created a container using ```docker run [*flags] image-name``` then you can start one by using the ```docker start container-name``` command. 

You can use the ```docker container ls -a``` command to view all containers (not just running ones) if you forget the container name.

## Sharing Work

You can either use ```docker save image_name``` for an image or ```docker export container_name``` for a container. This will output a tar (compressed) file to standard output, you can save this to a .tar file by piping ```docker export container_name > dk.container_name.latest.tar```. Then you can use ```docker load file``` or ```docker import file``` on a different machine.
