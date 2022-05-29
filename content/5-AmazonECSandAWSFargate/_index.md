---
title : "Deploy the container using AWS Fargate"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

#### Deploy the container using AWS Fargate

![Deploy the container using AWS Fargate](/images/1-Introduce/02-arch.png?featherlight=false&width=90pc)

1. First we will create **Task definitions** to run monolith

- Go to **[ECS](https://ap-southeast-1.console.aws.amazon.com/ecs/v2/task-definitions?region=ap-southeast-1)**
- Select **Task definitions**
- Find the Task definition named **Monolith-Definition-STACK_NAME**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0001-awsfargate.png?featherlight=false&width=90pc)

2. Go to **[ECR](https://ap-southeast-1.console.aws.amazon.com/ecr/repositories?region=ap-southeast-1)**

- Copy **Image URI**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0002-awsfargate.png?featherlight=false&width=90pc)

3. Back to interface **[ECS](https://ap-southeast-1.console.aws.amazon.com/ecs/v2/task-definitions?region=ap-southeast-1)**

- Select **Monolith-Definition-STACK_NAME**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0003-awsfargate.png?featherlight=false&width=90pc)

4. In the interface **Monolith-Definition-STACK_NAME** revision 1. We will create a new revision.

- Select **Create new revision**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0004-awsfargate.png?featherlight=false&width=90pc)

5. Configure **Container**

- **Name**, enter the service name of your choice (In the lab, enter **```monolith-service```**)
- Paste the copied **Image URI** into **Image URI**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0005-awsfargate.png?featherlight=false&width=90pc)

6. Select **Create**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0006-awsfargate.png?featherlight=false&width=90pc)

7. Finish creating a new revision

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0007-awsfargate.png?featherlight=false&width=90pc)

8. In view **Monolith-Definition-STACK_NAME** revision 2

- Select **Deploy**
- Select **Run task**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0008-awsfargate.png?featherlight=false&width=90pc)

9. In the **Deploy** interface

- **Environment**, select **Existing cluster**, select **Cluster-STACK_NAME**
- Select **Launch type**
- In **Launch type**, select **FARGATE**
- **Platform version** select **LATEST**
 
![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0009-awsfargate.png?featherlight=false&width=90pc)

10. In the **Deployment configuration** section

- Select **Task**
- **Desired** choose 1

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00010-awsfargate.png?featherlight=false&width=90pc)

11. Configure **Networking**

- **VPC**, select **Mysfits-VPC-STACK_NAME**
- **Subnets** select **Mysfits-PublicOne-STACK_NAME**
- Select **Security Group**, Select **Use an existing security group**
- **Security group name**, choose **default** but configure **inbound** port 80
- **Auto-assign public IP** - "ENABLED"
- Select **Deploy**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00011-awsfargate.png?featherlight=false&width=90pc)

12. Create task successfully

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00012-awsfargate.png?featherlight=false&width=90pc)

13. Select the task you just created and select **Networking**.

- Purpose of using **Public IP** to use **curl** command to check by making **GET request**.
- When using **Fargate** initialization, each task gets its own **ENI** and **Public IP** and **Private IP**.

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00013-awsfargate.png?featherlight=false&width=90pc)

14. Make a browser access

```
http://TASK_PUBLIC_IP_ADDRESS/mysfits
```

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00014-awsfargate.png?featherlight=false&width=90pc)

15. Execute the **curl** command on **Cloud9**

```
curl http://TASK_PUBLIC_IP_ADDRESS/mysfits
```


![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00015-awsfargate.png?featherlight=false&width=90pc)

16. Select the task you just created and select **Logs**
    
![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00016-awsfargate.png?featherlight=false&width=90pc)

17. Using AWS CloudWatch to View **Log events**

- Select **monolith log group** (**STACK_NAME-MythicalMonolithLogGroup-XXX**)

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00017-awsfargate.png?featherlight=false&width=90pc)

18. After running the **curl** command successfully, we can delete the task

- Select **Task**
- Select **Monolith-Definition-STACK_NAME** revision 2.
- Select **Stop**
- Select **Stop selected**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00018-awsfargate.png?featherlight=false&width=90pc)

19. Verify **Stop** and select **Stop**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00019-awsfargate.png?featherlight=false&width=90pc)

20. Delete task successfully.

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00020-awsfargate.png?featherlight=false&width=90pc)