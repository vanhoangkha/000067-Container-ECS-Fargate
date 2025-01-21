---
title : "ALB and ECS Service"
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

#### Scale the adoption platform monolith with an ALB and an ECS Service

![Scale the adoption platform monolith with an ALB and an ECS Service](/images/1-Introduce/03-arch.png?featherlight=false&width=90pc)

The Run Task method used in the previous section is great for testing, but if needed to run the platform apply it as a long-running process. You need to use **Elastic Load Balancing Application Load Balancer (ALB)** to deliver requests to your running containers. In addition to simple load balancing, it also creates capabilities such as path-based routing to different services.

**ECS** helps maintain the number of **desired tasks** (the number of containers running for a long time) and integrates **ALB** (handles the registration/deregistering of containers into the ALB)

The original ECS and ALB service was created by CloudFormation. In this lab, you will update those resources to host the encapsulated monolith service. Then you will create a new service from scratch after breaking the monolith.

1. Access to **CloudFormation**

- Select **STACK_NAME**
- Select **Stack details**
- Select **Outputs**
- Select **LoadBalancerDNS**

![Deploy the container using AWS Fargate](/images/6-ALB/0001-alb.png?featherlight=false&width=90pc)

2. Use your browser to access **LoadBalancerDNS**

![Deploy the container using AWS Fargate](/images/6-ALB/0002-alb.png?featherlight=false&width=90pc)

3. Go to **[ECS](https://ap-southeast-1.console.aws.amazon.com/ecs/v2/clusters?region=ap-southeast-1)**

- Select **Clusters**
- Select **Cluster-STACK_NAME**

![Deploy the container using AWS Fargate](/images/6-ALB/0003-alb.png?featherlight=false&width=90pc)

4. In the **Cluster-STACK_NAME** interface, we proceed to update **service**

- In the **Services** section, choose the lab service
- Click **Update**

![Deploy the container using AWS Fargate](/images/6-ALB/0004-alb.png?featherlight=false&width=90pc)

5. In the service update interface

- Select the latest **Revision**
- Click **Update**

![Deploy the container using AWS Fargate](/images/6-ALB/0005-alb.png?featherlight=false&width=90pc)

6. Service update is successful.

![Deploy the container using AWS Fargate](/images/6-ALB/0006-alb.png?featherlight=false&width=90pc)

7. In the **Cluster-STACK_NAME** interface

- Select **Task**
- Check **Monolith-Definition-STACK_NAME** has been updated to **Revision 22** (or any latest revision)

![Deploy the container using AWS Fargate](/images/6-ALB/0007-alb.png?featherlight=false&width=90pc)

8. Access to **CloudFormation**

- Select **STACK_NAME**
- Select **Stack details**
- Select **Outputs**
- Select **S3WebsiteURL**

![Deploy the container using AWS Fargate](/images/6-ALB/0008-alb.png?featherlight=false&width=90pc)

9. Use a browser to access **S3WebsiteURL**

![Deploy the container using AWS Fargate](/images/6-ALB/0009-alb.png?featherlight=false&width=90pc)

10. Perform user interface experience operations

![Deploy the container using AWS Fargate](/images/6-ALB/00010-alb.png?featherlight=false&width=90pc)

11. Access to **ECS**

- Select **Cluster**
- Select **Cluster-STACK_NAME**
- Select **Tasks**
- Select **Monolith-Definition-STACK_NAME** revision 2

![Deploy the container using AWS Fargate](/images/6-ALB/00011-alb.png?featherlight=false&width=90pc)

12. Select **Logs**

![Deploy the container using AWS Fargate](/images/6-ALB/00012-alb.png?featherlight=false&width=90pc)

13. Check the logs to make sure the monolith can read and write **DynamoDB** and can handle the like.

![Deploy the container using AWS Fargate](/images/6-ALB/00013-alb.png?featherlight=false&width=90pc)

14. Check CloudWatch logs from ECS to make sure **Like processed**

![Deploy the container using AWS Fargate](/images/6-ALB/00014-alb.png?featherlight=false&width=90pc)

15. Access **CloudWatch**

- Select **Log groups**
- Observe event log

![Deploy the container using AWS Fargate](/images/6-ALB/00015-alb.png?featherlight=false&width=90pc)

16. To distinguish between **service** and task. We can do the following steps:

- Select the service with the latest **Revision**
- Click **Update**

![Deploy the container using AWS Fargate](/images/6-ALB/00018-alb.png?featherlight=false&width=90pc)

17. Increase **Desired task** to 3 and update.

![Deploy the container using AWS Fargate](/images/6-ALB/00016-alb.png?featherlight=false&width=90pc)

18. After a successful update.

- Select **Task** to see 3 running tasks.
- From there, we see **ECS services** is a concept in which ECS allows running and maintaining a specific number of containers of task definitions in an ECS cluster. A service consists of many tasks and is maintained.

![Deploy the container using AWS Fargate](/images/6-ALB/00017-alb.png?featherlight=false&width=90pc)