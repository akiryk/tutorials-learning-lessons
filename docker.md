# Docker
These notes are for the Cloud Academy [Docker In Depth](https://cloudacademy.com/learning-paths/cloud-academy-docker-in-depth-129/) learning path.

## Introduction

### How to create a new image from a container
* Start with an image
* Run the image as a container
* Install some software into your container
* Convert the container to a new image

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
docker run ubuntu_python # will run the image as a container, which will output the python command





