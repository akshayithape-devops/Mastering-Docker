### Lab 2 : Create Docker Container for Apache Web Server

Video Link : https://www.youtube.com/watch?v=J5jAvJTiw68&t=187s

1. Run the container for Apache web server with port mapping.
2. Clean Up

---

#### 1. Run the container for Apache web server with port mapping

- Check Docker HTTPD image is available on local or not 

```
docker images
```

- Pull Apache HTTPD docker image

```
docker pull httpd
```

- Verify that Apache HTTPD docker image is pulled successfully or not

```
docker images
```

- Run container called `my-web`

```
docker run -d -p 8080:80 --name my-web httpd
```

- List running Docker processes

```
docker ps
```

- Test the webserver is deployed in a container or not 

```
curl http://localhost:8080
```

#### 2. Clean Up

- Stop running container

```
docker stop my-web
``` 

- Remove stop container

```
docker stop my-web
``` 

- Remove HTTPD docker image

```
docker rmi httpd
```
