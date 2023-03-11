### Lab 3 : Docker Volume Hands-on

---

1. Creating Volume Mount from Dockerfile
2. Managing volumes through Docker CLI
3. Creating Volume Mount from docker run command & sharing same Volume Mounts among multiple containers
4. Mounting host directory using bind mount into container

---

#### Creating Volume Mount from Dockerfile

* The VOLUME instruction creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers.

* Format :

```
VOLUME ["/data"]
```

* Hands-on Lab :

Create directory for labs

```
mkdir volumes
cd volumes
```

Create a file with name `volume` and paste the following content into it:

```
ARG CODE_VERSION=latest
FROM ubuntu:${CODE_VERSION}
RUN mkdir /data
WORKDIR /data
RUN echo "Hello from Volume" > test
VOLUME /data
```

Execute following commands:

```
docker build -f volume -t akshayithape02/volume:v1 .

docker run -it akshayithape02/volume:v1

docker volume ls

cd /var/lib/docker/volumes

cd ./<FOLDER_NAME_WITH_RANDOM_NUMBERS_&_CHARACTERS>

cd ./_data
 
cat test 
```

---

#### Managing volumes through Docker CLI

Execute following commands:

```
docker volume create demo

docker volume ls

docker inspect demo

docker volume rm demo
```

---

#### Creating Volume Mount from docker run command & sharing same Volume Mounts among multiple containers

Create a file with name `volume_test` and paste the following content:

```
ARG CODE_VERSION=latest
FROM ubuntu:${CODE_VERSION}
ENV MESSAGE=HI
ENV FILENAME=test
WORKDIR /data
ENTRYPOINT echo ${MESSAGE} > ${FILENAME} && ls
```

Execute following commands:

```
docker build -f volume_test -t akshayithape02/volume-test:v1 .

docker volume create demo

docker run --env MESSAGE="GOOD Morning" --env FILENAME=morning_message --mount type=volume,source=demo,target=/data akshayithape02/volume-test:v1

docker run --env MESSAGE="GOOD Afternoon" --env FILENAME=afternoon_message --mount type=volume,source=demo,target=/data akshayithape02/volume-test:v1

docker volume ls

cd /var/lib/docker/volumes/demo/_data

ls

cat morning_message &&  cat afternoon_message
```

#### Mounting host directory using bind mount into container

Execute following commands:

```
mkdir test-data

docker run --env MESSAGE="GOOD Afternoon" --env FILENAME=afternoon_message --mount type=bind,source="$(pwd)"/test-data,target=/data akshayithape02/volume-test:v1


cd ./test-data

ls 

cat afternoon_message
```
