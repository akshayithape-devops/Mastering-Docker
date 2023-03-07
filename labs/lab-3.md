### Lab 3 : Dockerfile Hands-on

---

1. FROM instruction
2. RUN instruction
3. CMD instruction
4. LABEL instruction
5. EXPOSE instruction
6. ENV instruction
7. ADD & COPY instruction
8. USER instruction
9. ENTRYPOINT instruction
10. WORKDIR instruction

---

#### Dockerfile Format 

```
# comment
INSTRUCTION arguments
OR 
COMMAND argumentss

# Example
RUN echo 'hello'
```

#### FROM Instruction

* It initializes a new build stage and sets the base image for subsequent instructions.
* A valid Dockerfile must start from a FROM instruction.
* ARG is the only instruction that precedes the FROM instruction.
* FROM can appear multiple times within a single Dockerfile to create multiple images or use one build stage as a dependency for another.
* Format :

```
FROM [--platform=<platform>] <image> [AS <name>]

OR 

FROM [--platform=<platform>] <image>[:<tag>] [AS <name>]

OR

FROM [--platform=<platform>] <image>[@<digest>] [AS <name>]
```

* Hands-on Lab :

Create a file with name `from` and paste the following content into it:

```
ARG CODE_VERSION=latest
FROM ubuntu:${CODE_VERSION}
```

Execute following commands:

```
docker build -f from -t akshayithape02/from:v1 .

docker run akshayithape02/from:v1 
```

#### RUN Instruction

* It will execute any commands in a new layer on top of the current image and commit the results. The resulting committed image will be used for the next step in the Dockerfile.
* Format :

```
RUN <command>
RUN ["executable", "param1", "param2"]
```

* Hands-on Lab :

Create a file with name `run` and paste the following content into it:

```
ARG CODE_VERSION=latest
FROM ubuntu:${CODE_VERSION}
RUN echo hello from shellform
RUN ["echo", "hello from execform"]
```

Execute following commands:

```
docker build -f run -t akshayithape02/run:v1 .

docker run akshayithape02/run:v1 
```

#### CMD Instruction

* There can only be one CMD instruction in a Dockerfile. If you list more than one CMD then only the last CMD will take effect.
* The main purpose of a CMD is to provide defaults for an executing container.
* Format :

```
CMD command param1 param2
CMD ["executable","param1","param2"]
CMD ["param1","param2"]
```

* Hands-on Lab :

Create a file with name `cmd` and paste the following content into it:

```
ARG CODE_VERSION=latest
FROM ubuntu:${CODE_VERSION}
CMD echo hello
```

Execute following commands:

```
docker build -f cmd -t akshayithape02/cmd:v1 .

docker run akshayithape02/cmd:v1 
```

#### LABEL Instruction

* The LABEL instruction adds metadata to an image. A LABEL is a key-value pair.
* docker inspect command is used to view the label’s
* Format :

```
LABEL <key>=<value> <key>=<value> <key>=<value> ...
```

* Hands-on Lab :

Create a file with name `label` and paste the following content into it:

```
ARG CODE_VERSION=latest
FROM ubuntu:${CODE_VERSION}
LABEL AUTHOR="Akshay Ithape"
```

Execute following commands:

```
docker build -f label -t akshayithape02/label:v1 .

docker run akshayithape02/label:v1 
```

#### EXPOSE Instruction

* The EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime.
* The EXPOSE instruction does not actually publish the port. It functions as a type of documentation between the person who builds the image and the person who runs the container, about which ports are intended to be published
* To actually publish the port when running the container, use the -p flag on docker run
* Format :

```
EXPOSE <port> [<port>/<protocol>...]
```

* Hands-on Lab :

Create a file with name `expose` and paste the following content into it:

```
ARG CODE_VERSION=latest
FROM tomcat:${CODE_VERSION}
EXPOSE 8080
```

Execute following commands:

```
docker build -f expose -t akshayithape02/expose:v1 .

docker run akshayithape02/expose:v1 
```

#### ENV Instruction

* The ENV instruction sets the environment variable  to the value . This value will be in the environment for all subsequent instructions in the build stage.
* The environment variables set using ENV will persist when a container is run from the resulting image.
* Format :

```
ENV <key>=<value> ...
```

* Hands-on Lab :

Create a file with name `env` and paste the following content into it:

```
ARG CODE_VERSION=latest
FROM ubuntu:${CODE_VERSION}
ENV NAME=Akshay
RUN echo ${NAME}
CMD echo ${NAME}
```

Execute following commands:

```
docker build -f env -t akshayithape02/env:v1 .

docker run akshayithape02/env:v1 
```

#### ADD & COPY Instruction

* COPY and ADD are both Dockerfile instructions that serve similar purposes. They let you copy files from a specific location into a Docker image.
* COPY takes in a src and destination. It only lets you copy in a local file or directory from your host (the machine building the Docker image) into the Docker image itself.
* ADD lets you do that too, but it also supports 2 other sources. First, you can use a URL instead of a local file / directory. Secondly, you can extract a tar file from the source directly into the destination.
* Format :

```
ADD [--chown=<user>:<group>] <src>... <dest>
ADD [--chown=<user>:<group>] ["<src>",... "<dest>"] (Use for Path Containing Whitespaces)

COPY [--chown=<user>:<group>] <src>... <dest>
COPY [--chown=<user>:<group>] ["<src>",... "<dest>"]
```

* Hands-on Lab :

Create a file with name `addcopy` and paste the following content into it:

```
ARG CODE_VERSION=latest
FROM ubuntu:${CODE_VERSION}
COPY ./copy/test_copy /
ADD ./add/test_add /
ADD https://golang.org/doc/install?download=go1.11.4.linux-amd64.tar.gz /
CMD cat test_copy && cat test_add && ls
```

Execute following commands:

```
docker build -f addcopy -t akshayithape02/addcopy:v1 .

docker run akshayithape02/addcopy:v1 
```

#### USER Instruction

* The USER instruction sets the user name (or UID) and optionally the user group (or GID) to use as the default user and group for the remainder of the current stage. 
* The specified user is used for RUN instructions and at runtime, runs the relevant ENTRYPOINT and CMD commands.

* Format :

```
USER <user>[:<group>]
USER <UID>[:<GID>]
```

* Hands-on Lab :

Create a file with name `user` and paste the following content into it:

```
ARG CODE_VERSION=latest
FROM ubuntu:${CODE_VERSION}
RUN groupadd -r user && useradd -r -g user user
USER user
```

Execute following commands:

```
docker build -f user -t akshayithape02/user:v1 .

docker run akshayithape02/user:v1 
```

#### ENTRYPOINT Instruction

* An ENTRYPOINT allows you to configure a container that will run as an executable.

* Format :

```
ENTRYPOINT ["executable", "param1", "param2"] (exec form, preferred)
ENTRYPOINT command param1 param2 (shell form)
```

* Hands-on Lab :

Create a file with name `entrypoint` and paste the following content into it:

```
ARG CODE_VERSION=latest
FROM ubuntu:${CODE_VERSION}
ENTRYPOINT ["echo", "hello"]
```

Execute following commands:

```
docker build -f entrypoint -t akshayithape02/entrypoint:v1 .

docker run akshayithape02/entrypoint:v1 
```

#### WORKDIR Instruction

* The WORKDIR instruction sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD instructions that follow it in the Dockerfile. If the WORKDIR doesn’t exist, it will be created even if it’s not used in any subsequent Dockerfile instruction.

* Format :

```
WORKDIR /path/to/workdir
```

* Hands-on Lab :

Create a file with name `workdir` and paste the following content into it:

```
ARG CODE_VERSION=latest
FROM ubuntu:${CODE_VERSION}
WORKDIR /data
RUN echo "hello" > test
ENTRYPOINT ["cat", "test"]
```

Execute following commands:

```
docker build -f workdir -t akshayithape02/workdir:v1 .

docker run akshayithape02/workdir:v1 
```