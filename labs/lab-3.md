### Lab 3 : Dockerfile Hands-on

---

1. FROM instruction
2. RUN instruction
3. CMD instruction
4. LABEL instruction
5. EXPOSE instruction
6. ENV instruction
7. ADD & COPY instruction
8. VOLUME instruction
9. ENTRYPOINT instruction
10. WORKDIR instruction

---

#### Dockerfile Format 

```
# comment
INSTRUCTION arguments

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