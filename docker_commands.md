1. find all available docker:
```
docker images
```
2. commit the current container to docker image:
```
docker commit --container_id --docker_image
```
5. tag the current docker image:
```
docker tag docker_name docker_tagged_name
```
7. push a docker image to server/hub:
```
docker push docker_tagged_name
```
9. steps to create a docker container from scratch: 1) build a docker (after writing the docker file), tag it and push it 2) run a docker

