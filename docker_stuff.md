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