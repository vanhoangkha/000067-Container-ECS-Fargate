---
title : "Docker Basics"
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---

#### Overview

Docker is a software platform that allows you to quickly build, test, and deploy applications. Docker packages software into standardized units called containers that have everything the software needs to run, including libraries, system tools, code, and runtimes. Using Docker, you can quickly deploy and scale your application into any environment and know with certainty that your code will run.
Running Docker on AWS gives developers and administrators a low-cost and highly reliable way to build, ship, and run distributed applications of any size.

{{% notice info %}}
Docker partners with AWS to help developers quickly bring modern applications to the cloud. This partnership helps developers using Docker Compose and Docker Desktop to leverage the same local workflows they use today to seamlessly deploy applications on Amazon ECS and AWS Fargate.
{{% /notice %}}

#### How Docker works

Docker works by providing a standard method for running your code. Docker is an operating system for containers. In the same way that a virtual machine virtualizes (eliminating the need to directly manage) server hardware, containers virtualize the host's operating system. Docker is installed on each host and provides simple commands that you can use to build, start, or stop containers.

AWS services like **AWS Fargate, Amazon ECS, Amazon EKS, and AWS Batch** make it easy to run Docker containers at scale.


![Docker basic](/images/1-Introduce/0001-docker.png?featherlight=false&width=60pc)


In the lab, we execute basic Docker commands with **AWS Cloud9**

1. Check the client and server are working with the command:

```bash
docker --version
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0001-dockerbasic.png?featherlight=false&width=90pc)

2. **Docker container** is built from **image**.

- command pull

```bash
docker pull [OPTIONS] NAME[: TAG|@DIGEST]
```

- First of all, we use the **docker pull nginx\:latest** command to pull the latest **nginx image** from **Docker Hub**.

```bash
docker pull nginx\:latest
```
 
![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0002-dockerbasic.png?featherlight=false&width=90pc)

3. To test pull the image successfully (**image will be in the local machine Docker cache**).

- Usage

```bash
docker images [OPTIONS] [REPOSITORY[: TAG]]
```

- Purpose of listing images.

```bash
docker images
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0003-dockerbasic.png?featherlight=false&width=90pc)

4. **Docker Daemon** acts as **server**, receives **RESTful requests** from **Docker Client** and executes.

- We use the command **docker run -d -p 8081:80 --name nginx nginx\:latest**.

```bash
docker run -d -p 8081:80 --name nginx nginx\:latest
```

- **-d**: May stand for "detached" - Run the container in the background
- Name the container as **nginx**
- **-p 8081:80**: Expose port 80 of container to port 8081 of machine **host**
- **nginx:latest**: Container launched from image is **nginx:latest**

- Reference command to run a container:

```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0004-dockerbasic.png?featherlight=false&width=90pc)

5. Check the **nginx** containers running with the command:

```bash
docker ps
```

- To perform the list of containers we execute the command:

```bash
docker ps [OPTIONS]
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0005-dockerbasic.png?featherlight=false&width=90pc)

6. Use command **curl http://localhost:8081** to use **nginx container** and verify it is working with **index.html**

```bash
curl http://localhost:8081
```

- Template for the **curl** command:

``` bash
curl [options/URLs]
```

{{% notice info %}}
Also you can read more about **[CURL](https://curl.se/)**
{{% /notice %}}


![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0006-dockerbasic.png?featherlight=false&width=90pc)

7. To view **nginx and container** logs.

- We use the **docker logs nginx** command. **curl request** event occurs

```bash
docker logs nginx
```

- Refer to the fetch log command of the container:

```bash
 docker logs [OPTIONS] CONTAINER
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0007-dockerbasic.png?featherlight=false&width=90pc)

8. Next, execute the command **docker exec -it nginx /bin/bash** to interact with **container filesystem and constraints**

```bash
docker exec -it nginx /bin/bash
```

- How to execute a command in a running container:

```bash
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0008-dockerbasic.png?featherlight=false&width=90pc)

9. We then proceed to view the content of nginx with the command:

```bash
cd /usr/share/nginx/html
cat index.html
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0009-dockerbasic.png?featherlight=false&width=90pc)

10. Use **exit** to get out

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/00010-dockerbasic.png?featherlight=false&width=90pc)

11. To stop running the container we execute the command

```bash
docker stop nginx
```

- Refer to the command to stop one or more containers:

```bash
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/00011-dockerbasic.png?featherlight=false&width=90pc)

12. Use **docker ps -a** to view container (including stopped container) to restart use command: **```docker start nginx```**

```bash
docker ps -a
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/00012-dockerbasic.png?featherlight=false&width=90pc)

13. Perform container deletion (input is container ID or container name)

```bash
docker rm nginx
```

- See the command to delete one or more containers:

```bash
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/00013-dockerbasic.png?featherlight=false&width=90pc)

14. Perform nginx image deletion with command (deleted image format can be **name: tag** or **IMAGE ID**)

```bash
docker rmi nginx\:latest
```
- Refer to the command to delete one or more images:

```bash
 docker rmi [OPTIONS] IMAGE [IMAGE...]
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/00014-dockerbasic.png?featherlight=false&width=90pc)