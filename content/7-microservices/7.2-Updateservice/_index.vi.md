---
title : "Cập nhật Service"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 7.2 </b> "
---

#### Cập nhật Service

1. Tiếp tục, truy cập vào **ECS**. Chúng ta sẽ tiến hành update service.

- Chọn **Cluster**
- Chọn **Cluster-STACK_NAME**

![ Microservices with AWS Fargate](/images/7-microservices/7.2-Updateservice/0001-updateservice.png?featherlight=false&width=90pc)

2. Trong cluster,

- Chọn **Service**
- Chọn **Service** hiện có (STACK_NAME-MythicalMonolithService-xxx)
- Chọn **Edit**

![ Microservices with AWS Fargate](/images/7-microservices/7.2-Updateservice/0002-updateservice.png?featherlight=false&width=90pc)

3. Thực hiện thay đổi revision mới nhất (revision chúng ta vừa tạo).

- Chọn **Update**


![ Microservices with AWS Fargate](/images/7-microservices/7.2-Updateservice/0003-updateservice.png?featherlight=false&width=90pc)

4. Như vậy, chúng ta đã tạo new revision và update service thành công.

![ Microservices with AWS Fargate](/images/7-microservices/7.2-Updateservice/0004-updateservice.png?featherlight=false&width=90pc)

5. Truy cập **ECS**

- Chọn **Cluster**
- Chọn **Service**
- Chọn **Monolith-Definition-STACK_NAME** revision 3.

![ Microservices with AWS Fargate](/images/7-microservices/7.2-Updateservice/0005-updateservice.png?featherlight=false&width=90pc)

6. Trong giao diện **Cluster-STACK_NAME**

- Chọn **Task**
- Chọn **Monolith-Definition-STACK_NAME** revision 3.

![ Microservices with AWS Fargate](/images/7-microservices/7.2-Updateservice/0006-updateservice.png?featherlight=false&width=90pc)


7. Kiểm tra Logs 

![ Microservices with AWS Fargate](/images/7-microservices/7.2-Updateservice/0007-updateservice.png?featherlight=false&width=90pc)
