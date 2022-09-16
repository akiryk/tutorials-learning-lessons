# Docker
These notes are for the Cloud Academy [Docker In Depth](https://cloudacademy.com/learning-paths/cloud-academy-docker-in-depth-129/) learning path.
This is a prerequisite for the [k8s course](https://github.com/cloudacademy/intro-to-k8s).

## Introduction

### Basics
```sh
# To see what images are on your maching
docker images

# See what containers are running
docker ps

# See what containers have run in the past
docker ps -a

# Remove a container and then an image
docker rm SOMECONTAINERID#
docker rmi SOMEIMAGE
```

### How to create a new image from a container
* Start with an image
* Run the image as a container
* Install some software into your container
* Convert the container to a new image and, optionally, change the default `CMD` command that will get run when you run the container. In this case, we'll change the default, which is `/bin/bash`, to one that will run some python code

In this example, we start with an Ubuntu image
```sh
# display all images
docker images

# run ubuntu as a container - this will start the container
docker run -it ubuntu /bin/bash

# update apt and install python3
root@c61f1448330a:/# apt update
root@c61f1448330a:/# apt install python3
# Exit so we can turn the container into an image
root@c61f1448330a:/# exit

# use `docker commit` to turn container into an image
# docker commit [change flag to change the CMD] [name_of_ubuntu_image] [new_name]
docker commit --change='CMD ["python3", "-c", "import this"]' c61f1448330a ubuntu_python
docker images # will list ubuntu_python as a new image
docker run ubuntu_python # will create a container based on this image, which will output the python command
```

### How to run a server from your container
Example with Go.

In order to run go, you need to have it installed. A good way to ensure you have what you need it to use the official Go image from docker hub, e.g. https://hub.docker.com/_/golang. 

1. Create Dockerfile:

Example Dockerfile
```
# Create build stage based on buster image
FROM golang:1.16-buster AS builder
# Create working directory under /app
WORKDIR /app
# Copy over all go config (go.mod, go.sum etc.)
COPY go.* ./
# Install any required modules
RUN go mod download
# Copy over Go source code
COPY *.go ./
# Run the Go build and output binary under hello_go_http
RUN go build -o /hello_go_http
# Make sure to expose the port the HTTP server is using
EXPOSE 8080
# Run the app binary when we run the container
ENTRYPOINT ["/hello_go_http"]
```

2. Build the image from the Dockerfile: `docker build -t myapp .` The `-t` is flag for the name of the app and the `.` says to make it from the current directory.
3. Run the image: `docker run -d -p 3000:8080 -t myapp`

## Networking
There are three networks
- Bridge, the default
- Host
- None
They all exist as networks only on the local host. There are additional types, however, that aren't only local.
