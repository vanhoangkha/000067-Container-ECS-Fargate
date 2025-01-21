---
title : "Dọn dẹp tài nguyên"
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

![Clean Stack CloudFormation](/images/8-Cleanup/0001-cleanup.png?featherlight=false&width=90pc)

6. Xác nhận xóa service.

![Clean Stack CloudFormation](/images/8-Cleanup/0001-cleanup-2.png?featherlight=false&width=70pc)

#### Xóa repository

1. Truy cập ECR: https://console.aws.amazon.com/ecr/repositories.

2. Chọn **Region** chứa repository
3. Chọn **Repository**
4. Chọn **Private** và chọn các repository liên quan bài lab.
5. Chọn **Delete**

![Clean Stack CloudFormation](/images/8-Cleanup/0002-cleanup.png?featherlight=false&width=70pc)

![Clean Stack CloudFormation](/images/8-Cleanup/0002-cleanup-2.png?featherlight=false&width=70pc)

#### Empty the S3 Bucket

1. Truy cập bảng điều khiển S3
2. Chọn **General purpose buckets** ở thanh điều hướng bên trái
3. Chọn Bucket của lab
4. Nhấn **Empty**
5. Gõ _Permanently delete_ để xác nhận
6. Nhấn **Delete**

![Clean Stack CloudFormation](/images/8-Cleanup/0004-cleanup.png?featherlight=false&width=90pc)

![Clean Stack CloudFormation](/images/8-Cleanup/0004-cleanup-2.png?featherlight=false&width=90pc)

#### Xóa CloudFormation Stack

1. Truy cập vào CloudFormation
2. Chọn **Stack**
3. Chọn stack liên quan bài lab. 
4. Chọn **Delete**

![Clean Stack CloudFormation](/images/8-Cleanup/0005-cleanup.png?featherlight=false&width=90pc)
