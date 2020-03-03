# <center> Docker for DataScience </center>

<p align="center"><img src="https://goto.docker.com/rs/929-FJL-178/images/Docker%20Horizontal%20Large.png"><p>

This a file is a consolidation of docker command and notes sourced form the community. Reference can be found at the bottom of page.

### Image Management


The following commands ares use for basis image management using docker.

```bash
# Pull down two docker images
docker pull debian
docker pull mysql/mysql-server

# View  images
docker images

# Remove all dangling images, volumes, and networks not associated  with a container
docker system prune

# Remove all unused images, volumes, and networks not associated  with a container
docker system prune -a

# View images (the results of the pruning)
docker images

# Remove one image
docker debian mysql/mysql-server

# Remove multiple image
docker rmi debian mysql/mysql-server
```


### The Basics

The the most vanilla commands in docker to start, stop, an attached to your docker containers.

```bash
# Stop docker container
docker stop tommy

# Start docker container
docker start tommy

# Reattached to started docker container
docker attach tommy
```

### Container Management

How to add, remove, and manage your docker containers

```bash
# View active docker containers
docker ps

# View all docker containers
docker ps -a

# Remove a docker container
docker rm tommy

# Remove more than one docker containe
docker rm tommy jeremy
```

### Saving and Loading Containers

Exporting your docker image and container and getting it ready for deployment

```bash
# Save container's image
docker export debian > debian_save.tar

# Save container data
docker export tommy  > tommy_export.tar

# Remove the activate container
docker stop tommy
docker rm tommy

# load image
docker load < debian_save.tar

# Import image data (with a new tag)
cat tommy_export.tar | docker import - debian:new

docker run --name douglas -it debian:new /bin/bash
```

### Docker Images Shortcuts

```bash
# Start a Linux Debian server
docker run --name tommy -it debian /bin/bash

# Start MYSQL database via docker
docker run -p 3306:3306 --name robert -e MYSQL_ROOT_PASSWORD=password -d mysql:5.7 --default-authentication-plugin=mysql_native_password

# Start an Apache Airflow Server via docker
docker run -d -p 8080:8080 -e LOAD_EX=y puckel/docker-airflow

# Start Apache Spark/Py Spark via docker
docker run -d -p 8888:8888 -v $PWD:/home/jovyan/work --name spark jupyter/pyspark-notebook
```

### File Transfer

The file transfer must be done from the host computer.
```bash
# Transfer file from host compute into docker container
# docker cp [Source] [Destination]
docker cp /Users/kavi/Desktop/test_image.png tommy:/root/

# Transfer an entire directory from our host machine to the docker container
docker cp ~/SSL  tommy:/root/SSL
```

### Stop, Start, and Attach to a container

```bash
# Stop the container
docker stop basic_container

# Start the container
docker start basic_container

# connect to the container
docker attach basic_container
```


### Stop & Remove docker containers

```bash
# Stop all Containers
docker kill $(docker ps -q)

# Remove all containers
docker rm $(docker ps -a -q)

# Remove all docker images
docker rmi $(docker images -q)
```

### References

The link below contain further reading on source references and documentation from the community on how to best use docker.


- https://docs.docker.com/engine/reference/commandline/import/
- https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes
- https://docs.docker.com/engine/reference/commandline/cp/
