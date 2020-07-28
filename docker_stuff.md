# Docker container backup

```
docker ps -a # to show all containers
```

it will display following message

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
fabaaf00cfc3        debian:8            "/bin/bash"         13 seconds ago      Up 11 seconds                           container1

## taking snapshot of specific container

```
docker commit -p fabaaf00cfc3 container1
```
The command above means paused running container fabaaf00cfc3 with -p option, made a commit to save the entire snapshot as a docker image with a name container1

# Docker delete image backup

list images
```
docker image ls [OPTIONS] [REPOSITORY[:TAG]]
```

pick the docker needs to be removed, then delete

```
docker image rm [image_name]
```
or
```
docker rmi IMAGE_ID
```

# Docker delete container

```
docker system prune
```
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all dangling images
  - all dangling build cache

or 

```
docker container rm [container_id]
```

# Pull image to local
```
docker pull IMAGE_NAME[:tag]
```

# Import/Export Images

## Export
```
docker save -o EXPORT_DIR IMAGE_ID
```

## Import
```
docker load -i IMAGE_FILE
```

# change docker tag name
```
docker tag IMAGE_ID TAG_NAME:VERSION
```

# Containers
## Run Container (Easy)
```
docker run IMAGE_ID|IMAGE_NAME[:tag]
```
## Run Container (Verbose)
```
docker run -d -p LOCAL_PORT:CONTAINER_PORT --name CONTAINER_NAME IMAGE_ID|IMAGE_NAME[:tag]
```
### -d: run the container at the back-end
### -p: map ports
### --name: assign name to the container

## Stop Container
### Stop specified container
```
docker stop CONTAINER_ID
```
or
### Stop all containers
```
docker stop $(docker ps -qa)
```

## Remove Contaienr
### Remove specified container
```
docker rm CONTAINER_ID
```
or
### Remove all containers
```
docker rm $(docker ps -qa)
```

# docker copy files
## From local to container
```
docker cp LOCAL_DIR/FILE_NAME CONTAINER_ID|CONTAINER_NAME:CONTAINER_TARGET_DIR
```
## From container to local
```
docker cp CONTAINER_ID|CONTAINER_NAME:CONTAINER_TARGET_DIR LOCAL_DIR/FILE_NAME
```

# docker volume
## create volume
```sh
# after creating the volume, it will be saved in a directory in the local machine
# linux: /var/lib/docker/volumes/VOLUME_NAME/_data
docker volume create VOLUME_NAME
```
## check volumn details
```
docker volume inspect VOLUME_NAME
```

## check all volumes
```
docker volume ls
```

## remove volume
```
docker volume rm VOLUME_NAME
```

## use volume 
```sh
# when mapping the volume, if it does not exist, docker will create it automatically
docker run -v VOLUME_NAME:VOLUME_CONTAINER_DIR IMAGE_ID
# nominate a dir for volume
docker run -v DIR:VOLUME_CONTAINER_DIR IMAGE_ID
```