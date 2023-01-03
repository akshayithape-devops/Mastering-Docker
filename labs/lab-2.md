### Lab 2 : Run Container For Java Application 

---

1. Build & Run Java application without using Docker
2. Build & Run Java application using Docker
3. Make changes Persistent
4. Push changes to Docker Hub
5. Rerun the container with new image(Persistent Changes)
6. Remove everything

---

#### 1. Build & Run Java application without using Docker(Optional)

> This part 1 require installed Java version 18.

- First we have to update play with docker virtual server. 
```
apk update
```

- We have to install java 
```
apk add openjdk11
```

- Clone the Java Application and Change the directory

```
git clone https://gist.github.com/akshayithape-devops/8e8128917a1754595cd155266d8f3aac.git
cd 8e8128917a1754595cd155266d8f3aac
```

- Now build java application with `javac` command.

```
javac helloworld.java
```

- Now run java application with `java` command.

```
java HelloWorld
```

#### 2. Build & Run Java application using Docker

- Run the Java container in Interactive mode

```
docker run -it --name javacontainer openjdk:18.0.2-jdk /bin/bash
```

> GIT & VIM editor is not installed. So we have to install it.

- Install GIT & VIM editor

```
microdnf install git vim
```

- Clone the Java Application and Change the directory

```
git clone https://gist.github.com/akshayithape-devops/8e8128917a1754595cd155266d8f3aac.git
cd 8e8128917a1754595cd155266d8f3aac
```

- Now build java application with `javac` command.

```
javac helloworld.java
```

- Now run java application with `java` command.

```
java helloworld.java
```

- Now we have update Java Application Code

```
vim helloworld.java

# Add following line in `System.out.println`

---
Welcome To Docker #101 - Hands-On Lab 2
---

# To save and exit 

:wq
```

- Now we have build new Java application Code

```
javac helloworld.java
```

- Run Java Application 

```
java HelloWorld
```

- We have move java binary to "/" directory

```
mv HelloWorld /
```

- Now exit the container

```
exit
```

#### 3. Make changes Persistent

- Commit the changes

```
docker commit --change='CMD ["java", "HelloWorld"]' javacontainer helloworld:v1
```

- Check the docker images

```
docker images
```

- Remove the container

```
docker rm javacontainer
```

- Run the container with new image 

```
docker run --name helloworldcontainer helloworld:v1
```

- Remove the container

```
docker rm helloworldcontainer
```

#### 4. Push changes to Docker Hub

- Docker login 

```
# Format
docker login -u username -p password/token
```

- Tag the docker image

```
docker tag helloworld:v1 akshayithape02/docker101-demo:v1
```

- List the docker image

```
docker images
```

- Push image to DockerHub

```
docker push akshayithape02/docker101-demo:v1
```

- Vist the docker hub and verify that your image is pushed or not

```
Browse https://hub.docker.com/
```

#### 5. Rerun the container with new image(Persistent Changes)

- Run the container with new image 

```
docker run --name helloworldcontainer akshayithape02/docker101-demo:v1
```

#### 6. Remove everything

- Clean up the containers
```
docker system prune
```

- Clean up the images
```
docker rmi -f $(docker images)
```

---