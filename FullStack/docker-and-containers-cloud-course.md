# Docker

- Create a new container running Ubuntu based on the docker image: `docker run -it ubuntu /bin/bash`
- You're now running an instance of this image, the Ubuntu
- change something in the container: add a file to `/home/`, `/home/akiryk/myfile.txt`
- Exit the container: `exit`
- See what containers are on your machine: `docker ps -a`
- Now open a new container with `docker run -it ubuntu /bin/bash`. The file you just created isn't there. THis is a NEW container based on the same "template" image
- Now open the previous container based on the name, e.g. `docker start quizzical_wing` followed by `docker attach quizzical_wing` (start and then enter)
- The file you created should be there.
