### Lab 3 : Create Docker Container for Apache Web Server with custom contents 

1. Run the container for web server with port & volume mapping.
2. Clean Up

---

#### 1. Run the container for web server with port & volume mapping.

- Create a working directory

```
mkdir lab-3 && cd lab-3
```

- Create index.html file 

```
echo "Welcome To Mastering Docker Session 1." > index.html
```

- Run container called `my-web-2`

```
docker run -d -p 8080:80 -v ./:/var/www/html --name my-web-2 httpd
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
docker stop my-web-2
``` 

- Remove stop container

```
docker stop my-web-2
``` 

- Remove HTTPD docker image

```
docker rmi httpd
```
