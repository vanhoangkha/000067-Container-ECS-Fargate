---
title : "Build Docker Image"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 7.3 </b> "
---

1. Access to **ECR**

- Select **Repository**
- Export 2 repositories **STACK_NAME-like-XXX** and **STACK_NAME-mono-XXX**

![ Microservices with AWS Fargate](/images/7-microservices/7.3-Builddockerimage/0001-builddockerimage.png?featherlight=false&width=90pc)

2. Now will build like service

```
 cd ~/environment/amazon-ecs-mythicalmysfits-workshop/workshop-1/app/like-service
 LIKE_ECR_REPOSITORY_URI=$(aws ecr describe-repositories | jq -r .repositories[].repositoryUri | grep like)
 docker build -t like-service .
```
![ Microservices with AWS Fargate](/images/7-microservices/7.3-Builddockerimage/0002-builddockerimage.png?featherlight=false&width=90pc)

3. Successfully execute docker image build then push to ECR with the latest tag.

```
 docker tag like-service:latest $LIKE_ECR_REPOSITORY_URI:latest
 docker push $LIKE_ECR_REPOSITORY_URI:latest
```

![ Microservices with AWS Fargate](/images/7-microservices/7.3-Builddockerimage/0003-builddockerimage.png?featherlight=false&width=90pc)

4. Executing the push successfully.

![ Microservices with AWS Fargate](/images/7-microservices/7.3-Builddockerimage/0004-builddockerimage.png?featherlight=false&width=90pc)

5. Check pushed image in **STACK_NAME-like-XXX**


![ Microservices with AWS Fargate](/images/7-microservices/7.3-Builddockerimage/0005-builddockerimage.png?featherlight=false&width=90pc)