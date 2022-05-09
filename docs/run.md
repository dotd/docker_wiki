# Running dockers
## To run a docker
Running docker **NOT** in interactive mode:
```
docker run -p80:3000 numpy-docker
docker container run -d [docker_image]
```

Running in **interactive** mode:
```
docker container run -it [docker_image] /bin/bash
# Detaching (Exiting) interactive mode CTRL+p && CTRL+q
# Attaching (Exiting) interactive mode 
# docker attach [container]
```

## checking Dockers
List running dockers:
```
# List:
docker ps
# List all:
docker ps -a
# Filtering
docker ps --filter "status=exited"
```

## Stopping Dockers
Stopping a docker:
```
docker run -p80:3000 numpy-docker
```
