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
3. Run multiple containers
4. Remove the containers

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

- Run the nginx container for demo 
```
docker run -d -p 8080:80 --name demo-container nginx:alpine
```

- Test the webserver is deployed in a container or not 
```
curl http://localhost:8080
```

> Now we have to see what happen in background. So lets create new container using Apache HTTPD image.

- List docker images
```
docker images
```

- Search docker image for Webserver(Apache HTTPD)
```
docker search httpd
```

- Pull Apache HTTPD docker image
```
docker pull httpd:alpine
```

- Verify that Apache HTTPD docker image is pulled successfully or not
```
docker images
```

- Run first container called `containerA`
```
docker run -d -p 8081:80 --name containerA httpd:alpine
```

- Test the webserver is deployed in a container or not 
```
curl http://localhost:8081
```

- List running Docker processes
```
docker ps
```

- To check the container logs
```
docker logs containerA
```

#### 3. Run multiple containers

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

- Run second container called `containerB`
```
docker run --name containerB hello-world:latest
```

- List running Docker processes
```
docker ps
```

- List all docker processes
```
docker ps -a
```

#### 4. Remove the containers

- Stop running container
```
docker stop containerA demo-container
``` 

- List all docker processes
```
docker ps -a
```

- Remove all containers
```
docker rm demo-container containerA containerB
```

- Verify whether docker containers removed or not 
```
docker ps -a
```

- Remove all docker images 
```
docker rmi nginx:alpine httpd:alpine hello-world:latest 

OR 

docker rmi $(docker images -a -q)
```

---
