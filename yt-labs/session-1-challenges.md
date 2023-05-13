## Docker Challenges 

### Challenge #1 : Run Commands Inside the Container 

---

- Create a Ubuntu container 
- Take access of shell
- Execute below commands on shell
    - echo 'Hello'
    - ps
    - top

### Challenge #2 : Check Container Log

---

- Create a Nginx container with port mapping  
- Then check the container log

### Challenge #3 : Check the Image Information

---

- Pull the `jenkins/jenkins:latest` image 
- Now check how many layers present inside the jenkins image.
- Also find the entrypoint of jenkins image.

### Challenge #4 : Build the Docker Image for HTML Application(Ref Lab 4) 

---

- Build docker image with following HTML contents.

![Challenge](../labs/images/Challenge-1.png)

- Publish that image on your Docker Hub Account.

### Challenge #5 : Take the Backup of newly created HTML Application Image into TAR.

--- 

- We have to take backup of newly created HTML application image into tar.
- File name should be `html-app.tar`


### Challenge #6 : Copy File into Container

---

- First create the container with port mapping.
- Run this command on local `echo "Hello, Pune" > index.html`
- Copy this index.html file into nginx container path `/usr/share/nginx/html/`
- Now in browser you should get `Hello, Pune`

---