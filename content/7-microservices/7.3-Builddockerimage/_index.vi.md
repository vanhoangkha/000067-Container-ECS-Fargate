---
title : "Build Docker Image"
weight : 3
chapter : false
pre : " <b> 7.3 </b> "
---

1.  Truy cập vào **ECR**

- Chọn **Repository**
- Xuất 2 repository **STACK_NAME-like-XXX** và **STACK_NAME-mono-XXX**

![ Microservices with AWS Fargate](/images/7-microservices/7.3-Builddockerimage/0001-builddockerimage.png?featherlight=false&width=90pc)

2.  Bây giờ sẽ build like service

```
 cd ~/environment/amazon-ecs-mythicalmysfits-workshop/workshop-1/app/like-service
 LIKE_ECR_REPOSITORY_URI=$(aws ecr describe-repositories | jq -r .repositories[].repositoryUri | grep like)
 docker build -t like-service .
```
![ Microservices with AWS Fargate](/images/7-microservices/7.3-Builddockerimage/0002-builddockerimage.png?featherlight=false&width=90pc)

3.  Thực hiện build docker image thành công sau đó push lên ECR với tag latest.

```
 docker tag like-service:latest $LIKE_ECR_REPOSITORY_URI:latest
 docker push $LIKE_ECR_REPOSITORY_URI:latest
```

![ Microservices with AWS Fargate](/images/7-microservices/7.3-Builddockerimage/0003-builddockerimage.png?featherlight=false&width=90pc)

4.  Thực hiện push thành công.

![ Microservices with AWS Fargate](/images/7-microservices/7.3-Builddockerimage/0004-builddockerimage.png?featherlight=false&width=90pc)

5.  Kiểm tra image đã được push trong **STACK_NAME-like-XXX**


![ Microservices with AWS Fargate](/images/7-microservices/7.3-Builddockerimage/0005-builddockerimage.png?featherlight=false&width=90pc)