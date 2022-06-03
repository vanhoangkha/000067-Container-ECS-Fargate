---
title : "Create CF Stack "
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

#### Create CloudFormation Stack

1. Go to [Deploy to AWS](https://ap-southeast-1.console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create?stackName=mysfits-fargate&templateURL=https://s3.amazonaws.com/mythical-mysfits-website/fargate/core.yml) to proceed with stack creation.

{{% notice note %}}
Alternatively, you can also create a CloudFormation Stack with Upload [yaml file](https://s3.amazonaws.com/mythical-mysfits-website/fargate/core.yml)
{{% /notice %}}

- The first step, configure the template. Select **Template is ready**
- **Template source**, select **Amazon S3 URL**
- In the lab, preconfigured **Amazon S3 URL**
- Select **Next**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0001-createcloudformation.png?featherlight=false&width=90pc)

2. We configure the stack details

- **Stack name**, enter the stack name you want to set.

{{% notice tip %}}
**STACK_NAME** will be used as the header or header of the names of the services in this lab. Example: **alb-STACK_NAME-XXX**
{{% /notice %}}
- In the **Parameters** section, select **false** for **SkipBucket**
- Select **Next**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0002-createcloudformation.png?featherlight=false&width=90pc)

3. Proceed to **Configure stack options**

- **Tags**, enter the value **key-value** (*you can enter it*)

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0003-createcloudformation.png?featherlight=false&width=90pc)

4. Select **Next**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0004-createcloudformation.png?featherlight=false&width=90pc)

5. Check configuration **stack**

- Select **I acknowledge that AWS CloudFormation might create IAM resources**
- Select **Create Stack**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0005-createcloudformation.png?featherlight=false&width=90pc)

6. Stack creation takes about **7 minutes**.

- Select **stack** to create successfully
- Select **Events**
- See the stack creation process

{{% notice info %}}
This stack initializes **Cloud9 Environment**, **DynamoDB Table**, **LoadBalancerDNS**, **ProfileName**, **S3WebsiteURL**, **SiteBucket**.
{{% /notice %}}

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0006-createcloudformation.png?featherlight=false&width=90pc)

7. In the newly created stack interface

- Select **Outputs**
- Select **value** as the path **Cloud9** of **Key** Cloud9Env.


![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0007-createcloudformation.png?featherlight=false&width=90pc)

8. We use **AWS Cloud9** as our development environment.

{{% notice note %}}
We will be using this **Cloud9 Environment** throughout the whole lab. The **AWS Cloud9 environment created by CloudFormation** is named **Project- STACK_NAME**
{{% /notice %}}

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0008-createcloudformation.png?featherlight=false&width=90pc)

9. Check **Outputs** of the stack

- Access to **S3**
- Select **Buckets**
- Bucket has been created (**http://BUCKET_NAME.s3-website.REGION.amazonaws.com/**)
- The website is static and the link is saved in **workshop-1/cfn-outputs.json**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0009-createcloudformation.png?featherlight=false&width=90pc)

10. Next we check **DynamoDB**

- Access to **DynamoDB**
- New **Table** has been initialized

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/00010-createcloudformation.png?featherlight=false&width=90pc)

11. Check **Load Balancers**

- Access to **EC2**
- Select **Load Balancers**
- Check the result

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/00011-createcloudformation.png?featherlight=false&width=90pc)