---
title : "Containerize the Mythical Mysfits monolith"
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

#### Containerize the Mythical Mysfits monolith

![Containerize monolith](/images/1-Introduce/01-arch.png?featherlight=false&width=90pc)

#### Meaning of an INSTRUCTION in Dockerfile.

- **FROM:** Used to indicate which image is built from the original image. Depending on the application that needs to be packaged, we will use a different original image.
- **RUN:** Used to run a command when building an image.
- **WORKDIR**: Used to set the working directory. Any subsequent RUN, CMD, ENTRYPOINT, COPY and ADD instructions will take place inside this WORKDIR directory.
- **COPY**: COPY the source directory from the host machine to the filesystem of the image.
- **CMD**: Used to provide the default command that will be run when the Docker Container starts from the built Image, there can only be 1 CMD directive.

1. Check **Dockerfile.draft**

```dockerfile
FROM ubuntu:20.04
RUN apt-get update -y
RUN apt-get install -y python3-pip python-dev build-essential
RUN pip3 install --upgrade pip
#[TODO]: Copy python source files and requirements file into container image

#[TODO]: Install dependencies listed in the requirements.txt file using pip3

#[TODO]: Specify a listening port for the container

#[TODO]: Run mythicalMysfitsService.py as the final step. We want this container to run as an executable. Looking at ENTRYPOINT and CMD for this?
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0001-monolith.png?featherlight=false&width=90pc)

2. Complete Dockerfile

```dockerfile
FROM ubuntu:20.04
RUN apt-get update -y
RUN apt-get install -y python3-pip python-dev build-essential
RUN pip3 install --upgrade pip
#[TODO]: Copy python source files and requirements file into container image
COPY ./service /MythicalMysfitsService
WORKDIR /MythicalMysfitsService
#[TODO]: Install dependencies listed in the requirements.txt file using pip3
RUN pip3 install -r ./requirements.txt
#[TODO]: Specify a listening port for the container
EXPOSE 80
#[TODO]: Run the mythicalMysfitsService.py as the final step
ENTRYPOINT ["python3"]
CMD ["mythicalMysfitsService.py"]
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0002-monolith.png?featherlight=false&width=90pc)

3. If the Dockerfile is complete, rename your file from "Dockerfile.draft" to "Dockerfile" and continue to the next step.

```bash
cd ~/environment/amazon-ecs-mythicalmysfits-workshop/workshop-1/app/monolith-service/
mv Dockerfile.draft Dockerfile
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0003-monolith.png?featherlight=false&width=90pc)

4. Execute build image with command **docker build [OPTIONS] PATH | URL | -** .

{{% notice note %}}
This command needs to be run in the same directory where your Dockerfile is located.
{{% /notice %}}

- Note the time after that for the build command to look in the current directory for the Dockerfile.

```bash
docker build -t monolith-service .
```


![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0004-monolith.png?featherlight=false&width=90pc)

5. You should see a bunch of results as Docker builds all the layers of the image.

{{% notice warning %}}
If something goes wrong during the build, the build will fail and stop (**red text and warnings along the way as long as the build doesn't fail**).
{{% /notice %}}

```bash
Removing intermediate container a71540b615b4
 ---> 5ab93ce927c8
Step 8/10 : EXPOSE 80
 ---> Running in 27074f1d4c3a
Removing intermediate container 27074f1d4c3a
 ---> f528fe7756d5
Step 9/10 : ENTRYPOINT ["python3"]
 ---> Running in 8ef1757aadb0
Removing intermediate container 8ef1757aadb0
 ---> a1d1ed159fb2
Step 10/10 : CMD ["mythicalMysfitsService.py"]
 ---> Running in da0c544e601b
Removing intermediate container da0c544e601b
 ---> b283e0821fc9
Successfully built b283e0821fc9
Successfully tagged monolith-service:latest
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0005-monolith.png?featherlight=false&width=90pc)

6. Your Dockerfile has been successfully created, but the Dockefile has not been optimized for microservices.

{{% notice info %}}
Since you convert monoliths into microservices, you will edit the source code (eg **mythicalMysfitsService.py**) and build this image a few times.
{{% /notice %}}

- Check Dockerfile

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0006-monolith.png?featherlight=false&width=90pc)

7. Dockerfile optimization

```dockerfile
FROM ubuntu:20.04
RUN apt-get update -y
RUN apt-get install -y python3-pip python-dev build-essential
RUN pip3 install --upgrade pip
COPY ./service/requirements.txt .
RUN pip3 install -r ./requirements.txt
COPY ./service /MythicalMysfitsService
WORKDIR /MythicalMysfitsService
EXPOSE 80
ENTRYPOINT ["python3"]
CMD ["mythicalMysfitsService.py"]
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0007-monolith.png?featherlight=false&width=90pc)

8. To see the benefits of Dockerfile optimization, you need to first **rebuild the monolith image** using the new Dockerfile.

```bash
docker build -t monolith-service .
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0008-monolith.png?featherlight=false&width=90pc)

9. Then we make changes to **mythicalMysfitsService.py** by adding a comment at the end of the file.

```python
# This is a comment to force a Docker-rebuild
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0009-monolith.png?featherlight=false&width=50pc)

10. Docker cached the requests on the first rebuild after reordering.

```bash
docker build -t monolith-service .
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00010-monolith.png?featherlight=false&width=90pc)

11. Perform rebuild monolith image again. Cache reference in this second rebuild

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00011-monolith.png?featherlight=false&width=90pc)

12. Use **docker images [OPTIONS] [REPOSITORY[:TAG]]** to list images

```bash
docker images
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00012-monolith.png?featherlight=false&width=60pc)

13. Run the container and test

```bash
export TABLE_NAME="$(jq < ~/environment/amazon-ecs-mythicalmysfits-workshop/workshop-1/cfn-output.json -r '.DynamoTable')"
docker run -p 8000:80 -e AWS_DEFAULT_REGION=$AWS_REGION -e DDB_TABLE_NAME=$TABLE_NAME monolith-service
```

{{% notice note %}}
Note: You can find your DynamoDB table names in the **workshop-1/cfn-output.json** file which is derived from the CloudFormation Stack output.
{{% /notice %}}

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00013-monolith.png?featherlight=false&width=90pc)

14. To test the basic functionality of a monolith service, query the service using a utility like **[cURL](https://curl.se/)** included with the linux distribution.

```bash
curl http://localhost:8000/mysfits
```

- You will see a JSON array with data about **Mythical Mysfits**

{{% notice note %}}
Note: Processes running inside a Docker container can authenticate with DynamoDB because they can access the EC2 Metadata API endpoint running at 169.254. attached to our Cloud9 environment in the initial setup script. Processes in the container cannot access the **~/.aws/credentials** file in the host filesystem (unless it's explicitly attached to the container).
{{% /notice %}}


![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00014-monolith.png?featherlight=false&width=90pc)

15. Back to the monolith container running tab

- Monolith container running in the foreground with stdout/stderr print to the screen, when receiving the request, will display **200 "OK"**

```bash
 * Serving Flask app "mythicalMysfitsService" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://0.0.0.0:80/ (Press CTRL+C to quit)
172.17.0.1 - - [26/May/2022 16:49:43] "GET /mysfits HTTP/1.1" 200 -
INFO:werkzeug:172.17.0.1 - - [26/May/2022 16:49:43] "GET /mysfits HTTP/1.1" 200 -
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00015-monolith.png?featherlight=false&width=90pc)

16. In the tab running monolith container, use the key combination **Ctrl + C** to stop running the container.

{{% notice note %}}
Note: Container runs in the foreground with stdout/stderr printing to the console. In a production environment, when running the container in the background and having to configure the destination of the logs. We can run the container in the background using **-d**.
{{% /notice %}}


```bash
export TABLE_NAME="$(jq < ~/environment/amazon-ecs-mythicalmysfits-workshop/workshop-1/cfn-output.json -r '.DynamoTable')"
docker run -d -p 8000:80 -e AWS_DEFAULT_REGION=$AWS_REGION -e DDB_TABLE_NAME=$TABLE_NAME monolith-service
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00016-monolith.png?featherlight=false&width=90pc)

17. List docker containers to check running containers

```bash
docker ps
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00017-monolith.png?featherlight=false&width=90pc)

18. See the running monolith in the list (store the Container ID to use docker logs). Repeat the **curl** command, then do a log check

```bash
docker logs <CONTAINER_ID>
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00018-monolith.png?featherlight=false&width=90pc)

19. Now, we have **Docker image** working, we do tag assignment and push to **ECR**. **AWS ECR** is a fully managed AWS Docker container registry service that simplifies the storage, management, and deployment of Docker container images.
**ECR** can be integrated with **Amazon Elastic Container Service (ECS)** to simplify deployment execution flow setup for production systems as well as eliminate management complexity. Repository manager for container images. Next, we use the ECS pull image from the ECR.

- Go to ECS and select **Repositories**
- We will have 2 repositories: **STACK_NAME-mono-xxx and STACK_NAME-like-xxx**
- Select the icon to copy **URL** of **Mono** repository (use in the next steps)

{{% notice note %}}
 Note: repository URI is unique
{{% /notice %}}

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00019-monolith.png?featherlight=false&width=90pc)

20. Implement tag assignment and push container image and monolith repository

```bash
MONO_ECR_REPOSITORY_URI=$(aws ecr describe-repositories | jq -r .repositories[].repositoryUri | grep mono)
docker tag monolith-service:latest $MONO_ECR_REPOSITORY_URI:latest
docker push $MONO_ECR_REPOSITORY_URI:latest
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00020-monolith.png?featherlight=false&width=90pc)

21. Visit the **ECR repository** page, the image is uploaded and tagged as the latest.

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00021-monolith.png?featherlight=false&width=90pc)