### Docker Command Format 

- Old Format 
```
docker <command> options
```

- New Format 
```
docker <management-command> <sub-command> options
```

### Lab 1 : Run your first container

1. Get docker information
2. Run a container
3. Remove the containers

---

#### 1. Get docker information

- Check version of docker
```
docker version
```

- Get more information about docker 
```
docker info
```

- Get help(It will display all the available commands)
```
docker help
```

#### 2. Run a container

- Check local images
```
docker images
```

- Search for `hello-world` docker image
```
docker search hello-world
```

- Pull hello-world docker image
```
docker pull hello-world:latest
```

- Verify that hello-world docker image is pulled successfully or not
```
docker images
```

- Run first container called `containerA`
```
docker run --name containerA hello-world:latest
```

- List running Docker processes
```
docker ps
```

- List all docker processes
```
docker ps -a
```

#### 3. Remove the containers

- Stop running container
```
docker stop containerA 
``` 

- List all docker processes
```
docker ps -a
```

- Remove all containers
```
docker rm containerA 
```

- Verify whether docker containers removed or not 
```
docker ps -a
```

- Remove all docker images 
```
docker rmi hello-world:latest 

OR 

docker rmi $(docker images -a -q)
```

---
