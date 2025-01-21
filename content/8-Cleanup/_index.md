---
title : "Clean up resources"
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

![Clean Stack CloudFormation](/images/8-Cleanup/0001-cleanup.png?featherlight=false&width=90pc)

6. Confirm delete service.

![Clean Stack CloudFormation](/images/8-Cleanup/0001-cleanup-2.png?featherlight=false&width=70pc)

#### Delete repository

1. Access ECR: https://console.aws.amazon.com/ecr/repositories.

2. Select **Region** containing the repository
3. Select **Repository**
4. Select **Private** and select the repositories related to the lab.
5. Select **Delete**

![Clean Stack CloudFormation](/images/8-Cleanup/0002-cleanup.png?featherlight=false&width=70pc)

![Clean Stack CloudFormation](/images/8-Cleanup/0002-cleanup-2.png?featherlight=false&width=70pc)

#### Empty the S3 Bucket

1. Enter S3
2. Select **General purpose buckets** on the left bar
3. Select the bucket of the lab
4. Click on **Empty**
5. Type _Permanently delete_ to confirm
6. Click on **Delete**

![Clean Stack CloudFormation](/images/8-Cleanup/0004-cleanup.png?featherlight=false&width=90pc)

![Clean Stack CloudFormation](/images/8-Cleanup/0004-cleanup-2.png?featherlight=false&width=90pc)

#### Clear CloudFormation Stack

1. Access to CloudFormation
2. Select **Stack**
3. Select the stack related to the lab.
4. Select **Delete**s

![Clean Stack CloudFormation](/images/8-Cleanup/0005-cleanup.png?featherlight=false&width=90pc)
