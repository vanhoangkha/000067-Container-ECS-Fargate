---
title : "Dọn dẹp tài nguyên"
date :  "`r Sys.Date()`" 
weight : 8 
chapter : false
pre : " <b> 8. </b> "
---

####  Dọn dẹp tài nguyên

#### Xóa ECS service

1. Mở bảng điều khiển Amazon ECS tại https://console.aws.amazon.com/ecs/.

2. Trên thanh điều hướng, chọn Region có cluster của bạn.

3. Trong ngăn dẫn hướng, hãy chọn Cluster và chọn tên của Cluster liên quan bài lab.

4. Trên trang Cluster, chọn **Service**

5. Chọn Delete.

6. Xác nhận xóa service.

![Clean up](/images/8-Cleanup/0001-cleanup.png?featherlight=false&width=90pc)

![Clean up](/images/8-Cleanup/0002-cleanup.png?featherlight=false&width=90pc)

![Clean up](/images/8-Cleanup/0003-cleanup.png?featherlight=false&width=90pc)


#### Xóa repository

1. Truy cập ECR :  https://console.aws.amazon.com/ecr/repositories.

2. Chọn **Region** chứa repository
3. Chọn **Repository**
4. Chọn **Private** và chọn các repository liên quan bài lab.
5. Chọn **Delete**

![Clean up](/images/8-Cleanup/0004-cleanup.png?featherlight=false&width=90pc)

#### Xóa ALB 

1. Truy cập vào EC2
2. Chọn **Load Balancer**
3. Chọn **ALB** của bài lab.
4. Chọn **Actions**
5. Chọn **Delete**

#### Xóa CloudFormation Stack

1. Truy cập vào CloudFormation
2. Chọn **Stack**
3. Chọn stack liên quan bài lab. 
4. Chọn **Delete**
