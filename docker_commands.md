1. steps to create a docker container from scratch:
step 1: build.sh file: build a docker (after writing the docker file), tag it and push it
step 2: run a docker

2. workflow in CMD for multiple GPUs (goal: create #gpus independent running consoles in the background (session interrupted even after closing the tab) from 1 source docker image)

step 1: 1) tmux new session 2) run docker 3) and then detach it (leave it alone all the time!) - **this is your general debugging container** - all GPUs are visible

step 2: 1) tmux new session 2) run docker_multiple gpus (i.e. docker run -d --gpus device=$i --name gpu_i xxx) 3) detach it. **this creates #gpus containers that is used for running scripts**

step 3: 1) tmux new session 2) attach docker for gpu_i created in step 2

step 4-x: repeat step 3 for the number of gpus.

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

