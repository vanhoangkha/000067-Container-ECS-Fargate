---
title : "Create Task Definition"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b>7.4 </b> "
---

#### Create Task Definition

1. Create **Task Definition** for like service using image pushed to ECR.

- In the **ECS** interface, select **Task definitions**
- Select **Create new task definition**
  

![ Microservices with AWS Fargate](/images/7-microservices/7.4-CreateTaskDefinition/0001-createtaskdefinition.png?featherlight=false&width=90pc)

2. Configure **Task definition**

- Set **Task definition family**, enter **Microservice-Definition-STACK_NAME**

![ Microservices with AWS Fargate](/images/7-microservices/7.4-CreateTaskDefinition/0002-createtaskdefinition.png?featherlight=false&width=90pc)

3. We use the image pushed to **ECR** in the repository **STACK_NAME-like-XXX**

- Like service code designed to call an endpoint on a monolith to persist data with **DynamoDB**. Reference the value of the **MONOLITH_URL** environment. We will create the environment with the Key of **MONOLITH_URL** and Value of **ALB** (specifically alb-STACK_NAME-XXX)
- Select **Next**

![ Microservices with AWS Fargate](/images/7-microservices/7.4-CreateTaskDefinition/0003-createtaskdefinition.png?featherlight=false&width=90pc)

5. Perform environment configuration

- We use **AWS Fargate**
- **Operating system** is Linux
- You can customize the Task size
- Select **Task role**, select **STACK_NAME-EcsServiceRole-XXX**

![ Microservices with AWS Fargate](/images/7-microservices/7.4-CreateTaskDefinition/0004-createtaskdefinition.png?featherlight=false&width=90pc)

6. Use **Amazon CloudWatch**

![ Microservices with AWS Fargate](/images/7-microservices/7.4-CreateTaskDefinition/0005-createtaskdefinition.png?featherlight=false&width=90pc)

7. Check again and select **Create**

![ Microservices with AWS Fargate](/images/7-microservices/7.4-CreateTaskDefinition/0006-createtaskdefinition.png?featherlight=false&width=90pc)

8. Thus, we have successfully created a Task definition **Microservice-Definition-STACK_NAME**

![ Microservices with AWS Fargate](/images/7-microservices/7.4-CreateTaskDefinition/0007-createtaskdefinition.png?featherlight=false&width=90pc)