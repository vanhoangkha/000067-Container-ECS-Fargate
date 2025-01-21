---
title : "Tạo Task Definition"
weight : 4
chapter : false
pre : " <b> 7.4 </b> "
---

#### Tạo Task Definition

1. Thực hiện tạo **Task Definition** cho like service sử dụng image đã push lên ECR.

- Trong giao diện **ECS**, chọn **Task definitions**
- Chọn **Create new task definition**
  

![ Microservices with AWS Fargate](/images/7-microservices/7.4-CreateTaskDefinition/0001-createtaskdefinition.png?featherlight=false&width=90pc)

2.  Tiến hành cấu hình **Task definition**

- Đặt **Task definition family**, nhập **Microservice-Definition-STACK_NAME**

![ Microservices with AWS Fargate](/images/7-microservices/7.4-CreateTaskDefinition/0002-createtaskdefinition.png?featherlight=false&width=90pc)

3.  Chúng ta sử dụng image đã push lên **ECR** trong repository **STACK_NAME-like-XXX**

- Like service code được thiết kế gọi endpoint trên monolith để duy trì dữ liệu với **DynamoDB**. Tham chiếu giá trị của môi trường **MONOLITH_URL**. Chúng ta sẽ tạo môi trường với Key là **MONOLITH_URL** và Value là **ALB**(cụ thể là alb-STACK_NAME-XXX)
- Chọn **Next**

![ Microservices with AWS Fargate](/images/7-microservices/7.4-CreateTaskDefinition/0003-createtaskdefinition.png?featherlight=false&width=90pc)

4.  Thực hiện cấu hình môi trường

- Chúng ta sử dụng **AWS Fargate**
- **Operating system** là Linux
- Bạn có thể tùy chỉnh Task size
- Chọn **Task role**, chọn **STACK_NAME-EcsServiceRole-XXX**

![ Microservices with AWS Fargate](/images/7-microservices/7.4-CreateTaskDefinition/0004-createtaskdefinition.png?featherlight=false&width=90pc)

5.  Tìm tên log group của lab trong CloudFormation stack, sao chép physical ID và dán vào giá trị của khóa `awslogs-group`

![ Microservices with AWS Fargate](/images/7-microservices/7.4-CreateTaskDefinition/0005-createtaskdefinition.png?featherlight=false&width=90pc)

6.  Kiểm tra lại và chọn **Create**

![ Microservices with AWS Fargate](/images/7-microservices/7.4-CreateTaskDefinition/0006-createtaskdefinition.png?featherlight=false&width=90pc)

7.  Như vậy, chúng ta đã tạo thành công một Task definition **Microservice-Definition-STACK_NAME**

![ Microservices with AWS Fargate](/images/7-microservices/7.4-CreateTaskDefinition/0007-createtaskdefinition.png?featherlight=false&width=90pc)