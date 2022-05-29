---
title : "Container image"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
---

#### Execute container image

In this part, we build the container image. Working with Dockerfiles.

Dockerfile is a text file with no extension, containing specifications for a software executable field, and structure for Docker Image. From those commands, Docker will build a Docker image (usually from a few MB to a few GB in size).

#### Dockerfile overview

The general syntax of a **Dockerfile**

```
INSTRUCTION arguments
```

- **INSTRUCTION** is the name of the directives contained in **Dockerfile**, each directive performing a certain task, specified by Docker.
- When declaring these directives, they must be written in **CAPITAL**.
- A **Dockerfile** must begin with the **FROM** directive to declare which image will be used as the background to build your image.
- **arguments** is the body of the directives, which decides what the directive will do.

#### Some directives in Dockerfile

**FROM**

```
FROM <image> [AS <name>]
FROM <image>[:<tag>] [AS <name>]
FROM <image>[@<digest>] [AS <name>]
```

**LABEL**

```
LABEL <key>=<value> <key>=<value> <key>=<value> ... <key>=<value> 
```

**MAINTAINER**

```
MAINTAINER <name> [<email>]
```

**RUN**

```
RUN <command>
```

**ADD**

```
ADD [--chown=<user>:<group>] <src>... <dest>
ADD [--chown=<user>:<group>] ["<src>",... "<dest>"]
```
**COPY**

```
COPY [--chown=<user>:<group>] <src>... <dest>
COPY [--chown=<user>:<group>] ["<src>",... "<dest>"]
```
**ENV**

```
ENV <key>=<value> ...
```
**CMD** Used to provide default command to be run when Docker Container starts from built Image, there can be only 1 CMD directive.

#### Practice

1. Create a folder for container image

```
mkdir ~/environment/container-image
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0001-containerimage.png?featherlight=false&width=90pc)

2. Type **cd container-image** to change into that directory.

```
cd ~/environment/container-image
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0002-containerimage.png?featherlight=false&width=90pc)

3. Run **touch Dockerfile** to create the Dockerfile. This file will contain a set of steps needed to build the container image.

```
touch Dockerfile
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0003-containerimage.png?featherlight=false&width=90pc)

4. Run below command to update Dockerfile content

```
cat <<EOF> Dockerfile
FROM nginx\:latest
COPY index.html /usr/share/nginx/html
EOF
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0004-containerimage.png?featherlight=false&width=90pc)

5. Run **touch index.html** to create an empty html file that will contain a simple message.

```
touch index.html
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0005-containerimage.png?featherlight=false&width=90pc)

6. Use **echo** to pass a simple message into the **index.html** file

```
echo "We've added our own custom content into the container" >> index.html
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0006-containerimage.png?featherlight=false&width=90pc)

7. Use **docker build -t nginx:1.0 .** to build the nginx container image from the Dockerfile.

```
docker build -t nginx:1.0 .
```

- Refer to the build image command from a Dockerfile

```
docker build [OPTIONS] PATH | URL | -
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0007-containerimage.png?featherlight=false&width=90pc)

8. Use **docker history nginx:1.0** to see all steps and base container.

```
docker history nginx:1.0
```

- Refer to the command to view the history of an image:

```
docker history [OPTIONS] IMAGE
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0008-containerimage.png?featherlight=false&width=90pc)

9. Use the command **docker run -p 8080:80 --name nginx nginx:1.0** to run the container (don't use background mode for easy debugging)

```
docker run -p 8080:80 --name nginx nginx:1.0
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0009-containerimage.png?featherlight=false&width=90pc)

10. Open another **Terminal** tab ( **Window -> New Terminal** ). Run **curl http://localhost:8080** in the tab a few times and see what's new.

```
curl http://localhost:8080
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00010-containerimage.png?featherlight=false&width=90pc)

11. Go back to the first tab and see the log lines sent immediately to STDOUT. Type **Ctrl-C** to exit the log output. Note that the container has been stopped but is still there when running **docker ps -a**.

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00011-containerimage.png?featherlight=false&width=90pc)

12. Using **docker ps -a**

```
docker ps -a
```
![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00012-containerimage.png?featherlight=false&width=90pc)

13. Use **sudo docker inspect nginx** to see detailed information about stopped containers.

```
sudo docker inspect nginx
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00013-containerimage.png?featherlight=false&width=90pc)

14. Use **docker rm nginx** to delete the container

```
docker rm nginx
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00014-containerimage.png?featherlight=false&width=90pc)

15. Mount some files from the host into the container instead of embedding them in the image.

```
docker run -d -p 8080:80 -v /home/ec2-user/environment/container-image/index.html:/usr/share/nginx/html/index.html\:ro --name nginx nginx\: latest
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00015-containerimage.png?featherlight=false&width=90pc)

16. Execute **curl http://localhost:8080**. Note that although this is an upstream nginx image from Docker Hub, the content is there.

```
curl http://localhost:8080
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00016-containerimage.png?featherlight=false&width=90pc)

17. Edit the index.html. file

```
echo "This is another line I've added to my container" >> index.html
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00017-containerimage.png?featherlight=false&width=90pc)

18. Try again **curl http://localhost:8080**

```
curl http://localhost:8080
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00018-containerimage.png?featherlight=false&width=90pc)

19. Finally, run **docker stop nginx** and **docker rm nginx** to stop and remove the container

```
docker stop nginx && docker rm nginx
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00019-containerimage.png?featherlight=false&width=90pc)