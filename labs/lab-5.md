### Lab 5 : Docker Networking Hands-on

---

1. Creating bridge network through Docker CLI
2. Connecting User Defined Network with container
3. Establishing connection between containers using bridge network
4. Connecting Host Network with container
5. Connecting None Network with container

---

#### Creating bridge network through Docker CLI

Execute the following commands:

```
docker network ls

docker network create -d bridge my-net-1

docker network create my-net-2 

docker network ls

docker network rm my-net-1 my-net-2
```

---

#### Connecting User Defined Network with container

Execute the following commands:

```
docker network create my-net-1

docker run --network my-net-1 -p 8080:80 -d  --name containerA httpd:latest

docker inspect containerA

docker network inspect my-net-1

docker stop containerA

docker rm containerA
```

---

#### Establishing connection between containers using bridge network

Execute the following commands:

```
docker run --name containerA -d -p 8080:8080 tomcat:latest

docker run --name containerB -d -p 8081:8080 tomcat:latest

docker inspect containerA

docker inspect containerB

// Note the IP Address for both containers from the output of above commands

docker exec -it containerA /bin/bash

apt-get update

apt-get install iputils-ping

ping <IP_ADDRESS_CONTAINER_B>

ping www.google.com

ping containerB

exit

docker exec -it containerB /bin/bash

apt-get update

apt-get install iputils-ping

ping <IP_ADDRESS_CONTAINER_A>

ping www.google.com

ping containerA

exit

docker network create my-net-a

docker network connect my-net-a containerA

docker network connect my-net-a containerB

docker inspect containerA

docker inspect containerB

// Note the IP Address for both containers from the output of above commands

docker exec -it containerA /bin/bash

ping <IP_ADDRESS_CONTAINER_B>

ping containerB

ping www.google.com

exit

docker exec -it containerB /bin/bash

ping <IP_ADDRESS_CONTAINER_A>

ping containerA

ping www.google.com

exit

docker network disconnect my-net-a containerA

docker network disconnect my-net-a containerB

docker container stop containerA containerB

docker container rm containerA containerB

docker network rm my-net-a
```

---

#### Connecting Host Network with container

Execute the following commands:

```
docker network ls

docker run -d --network host --name containerA tomcat:latest

curl localhost

docker stop containerA

docker rm containerA
```

---

#### Connecting None Network with container

Execute the following commands:

```
docker network ls

docker run -d --network node --name containerA tomcat:latest

docker exec -it containerA /bin/bash

docker inspect containerA

docker stop containerA

docker rm containerA
```