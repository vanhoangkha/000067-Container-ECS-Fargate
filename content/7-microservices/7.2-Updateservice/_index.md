---
title : "Update Service"
weight : 2
chapter : false
pre : " <b> 7.2 </b> "
---

#### Update Service

1. Continue, access **ECS**. We will proceed to update the service.

- Select **Cluster**
- Select **Cluster-STACK_NAME**

![Microservices with AWS Fargate](/images/7-microservices/7.2-Updateservice/0001-updateservice.png?featherlight=false&width=90pc)

2. In the cluster,

- Select **Service**
- Select the existing **Service** (STACK_NAME-MythicalMonolithService-xxx)
- Select **Update**

![ Microservices with AWS Fargate](/images/7-microservices/7.2-Updateservice/0002-updateservice.png?featherlight=false&width=90pc)

3. Make changes to the latest revision (the one we just created).

- Select **Update**


![ Microservices with AWS Fargate](/images/7-microservices/7.2-Updateservice/0003-updateservice.png?featherlight=false&width=90pc)

4. Thus, we have successfully created a new revision and updated the service.

![ Microservices with AWS Fargate](/images/7-microservices/7.2-Updateservice/0004-updateservice.png?featherlight=false&width=90pc)

5. Access **ECS**

- Select **Cluster**
- Select **Service**
- Select **Monolith-Definition-STACK_NAME** revision 23.

![ Microservices with AWS Fargate](/images/7-microservices/7.2-Updateservice/0005-updateservice.png?featherlight=false&width=90pc)

6. In the **Cluster-STACK_NAME** interface

- Select **Task**
- Select **Monolith-Definition-STACK_NAME** revision 3.

![ Microservices with AWS Fargate](/images/7-microservices/7.2-Updateservice/0006-updateservice.png?featherlight=false&width=90pc)


7. Check Logs

![ Microservices with AWS Fargate](/images/7-microservices/7.2-Updateservice/0007-updateservice.png?featherlight=false&width=90pc)