1. steps to create a docker container from scratch:
step 1: build.sh file: build a docker (after writing the docker file), tag it and push it
step 2: run a docker

2. workflow in CMD for multiple GPUs
step 1: create a base docker using tmux and then detach it (leave it alone all the time!)
step 2: create a new session in tmux and attach to the base docker (i.e. docker_gpu1)

4. find all available docker:
```
docker images
```
3. commit the current container to docker image (not inside docker but outside terminal):
```
docker commit --container_id --docker_image
```
4. tag the current docker image:
```
docker tag docker_name docker_tagged_name
```
5. push a docker image to server/hub:
```
docker push docker_tagged_name
```
6. check docker container id
open a external terminal (not inside docker)
```
docker ps
```
7. attach to an existing docker
```
docker attach container_id
```

