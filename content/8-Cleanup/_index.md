---
title : "Clean up resources"
date : "`r Sys.Date()`"
weight : 8
chapter : false
pre : " <b> 8. </b> "
---

#### Clean up resources

#### Remove ECS service

1. Open the Amazon ECS console at https://console.aws.amazon.com/ecs/.

2. On the navigation bar, select the Region where your cluster is located.

3. In the navigation pane, select Cluster and select the name of the Cluster associated with the lab.

4. On the Cluster page, select **Service**

5. Select Delete.

6. Confirm delete service.

![Clean up](/images/8-Cleanup/0001-cleanup.png?featherlight=false&width=90pc)

![Clean up](/images/8-Cleanup/0002-cleanup.png?featherlight=false&width=90pc)

![Clean up](/images/8-Cleanup/0003-cleanup.png?featherlight=false&width=90pc)


#### Delete repository

1. Access ECR: https://console.aws.amazon.com/ecr/repositories.

2. Select **Region** containing the repository
3. Select **Repository**
4. Select **Private** and select the repositories related to the lab.
5. Select **Delete**

![Clean up](/images/8-Cleanup/0004-cleanup.png?featherlight=false&width=90pc)

#### Delete ALB

1. Access to EC2
2. Select **Load Balancer**
3. Select **ALB** of the lab.
4. Select **Actions**
5. Select **Delete**

#### Clear CloudFormation Stack

1. Access to CloudFormation
2. Select **Stack**
3. Select the stack related to the lab.
4. Select **Delete**s