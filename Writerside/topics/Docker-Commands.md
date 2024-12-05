# Commands

Here is a list of commonly used Docker commands along with examples:

## 1. `docker run`
Runs a command in a new container.
```sh
docker run -d -p 80:80 nginx
```

## 2. `docker ps`
Lists running containers.
```sh
docker ps
```

## 3. `docker images`
Lists all images.
```sh
docker images
```

## 4. `docker pull`
Pulls an image from a registry.
```sh
docker pull ubuntu
```

## 5. `docker build`
Builds an image from a Dockerfile.
```sh
docker build -t myapp .
```

## 6. `docker stop`
Stops one or more running containers.
```sh
docker stop <container_id>
```

## 7. `docker start`
Starts one or more stopped containers.
```sh
docker start <container_id>
```

## 8. `docker rm`
Removes one or more containers.
```sh
docker rm <container_id>
```

## 9. `docker rmi`
Removes one or more images.
```sh
docker rmi <image_id>
```

## 10. `docker exec`
Runs a command in a running container.
```sh
docker exec -it <container_id> /bin/bash
```

## 11. `docker logs`
Fetches the logs of a container.
```sh
docker logs <container_id>
```

## 12. `docker network`
Manages Docker networks.
```sh
docker network create mynetwork
```

## 13. `docker volume`
Manages Docker volumes.
```sh
docker volume create myvolume
```

## 14. `docker-compose`
Runs multi-container Docker applications.
```sh
docker-compose up
```

## 15. `docker inspect`
Displays detailed information on Docker objects.
```sh
docker inspect <container_id>
```

## 16. `docker tag`
Creates a tag for an image.
```sh
docker tag <image_id> myrepo/myimage:tag
```

## 17. `docker push`
Pushes an image to a registry.
```sh
docker push myrepo/myimage:tag
```

## 18. `docker login`
Logs in to a Docker registry.
```sh
docker login
```

## 19. `docker logout`
Logs out from a Docker registry.
```sh
docker logout
```

These commands cover a wide range of Docker functionalities, from managing containers and images to working with networks and volumes.