---
title : "Create your CloudFormation Stack "
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

#### Create CloudFormation Stack

1. Use the online [Argon2 Hash Generator](https://www.coderstool.com/argon2-hash-generator) to generate the hashed password for the VSCode Server.

    - Enter your **unhashed** password. Save that password for later uses when you log into the IDE.
    - Ensure the following parameters, or your password will be unusable:

        - Parallelism Factor: 1
        - Memory Cost: 4096
        - Iterations: 3
        - Hash Length: 16
        - Hash Type: Argon2i

    - Click **Generate Hash**
    - Copy the **hashed** password. Save it so you would enter it during the CloudFormation Stack creation.

    <!-- ![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/argon2.png?featherlight=false&width=90pc) -->

2. Go to [the CloudFormation Console](https://ap-southeast-1.console.aws.amazon.com/cloudformation/home?region=ap-southeast-1) to proceed with stack creation.

<!-- ![CFN Console](/images/2-Prerequiste/2.1-CreateCloudFormation/0001-cloudformationmenu.png) -->

Use [this yaml file](/workloads/core.yaml) to deploy your CloudFormation stack.

- The first step, configure the template. Select **Template is ready**
- **Template source**, select **Amazon S3 URL**
- In the lab, preconfigured **Amazon S3 URL**
- Click **Next**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0001-createcloudformation.png?featherlight=false&width=90pc)

3. We configure the stack details

- **Stack name**, enter the stack name you want to set.

{{% notice tip %}}
**STACK_NAME** will be used as the header or header of the names of the services in this lab. Example: **alb-STACK_NAME-XXX**
{{% /notice %}}

- In the **Parameters** section:

    - For **IdeAmiId**, the default value is the latest Amazon Linux 2023 AMI. You can replace it with another AMI as you desire.
    
    - Enter an **instance type**. To minimize cost, keep the `t2.micro`(free-tier eligible) or `t3.micro`. For better performance, it is **Recommended** to use `t3.small` or larger types instead.
    
    - Select **false** for **SkipBucket**

    - For **VSCodeServerVersion**, enter your desired version (without the "v" at the beginning). You can see the list of versions [here](https://github.com/coder/code-server/releases).

- Click **Next**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0002-createcloudformation.png?featherlight=false&width=90pc)

4. Proceed to **Configure stack options**

    - **Tags**, enter the value **key-value** (*you can enter it*)

    ![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0003-createcloudformation.png?featherlight=false&width=90pc)

    - **Stack failure options** - Choose how you want your stack to behave on failure.

    ![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0003-createcloudformationbehaviour.png?featherlight=false&width=90pc)

5. Tick the checkbox on **I acknowledge that AWS CloudFormation might create IAM resources**, then click **Next**.

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0004-createcloudformation.png?featherlight=false&width=90pc)

6. Check your **stack** configuration . When you're satisfied, click **Submit**.

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0005-createcloudformation.png?featherlight=false&width=90pc)

7. Stack creation takes about **7 minutes**. When done, the status is switched to **CREATE_COMPLETE**.

{{% notice info %}}
This stack initializes **An EC2 instance with VSCode Server IDE installed**, **a DynamoDB Table**, **LoadBalancerDNS**, **ProfileName**, **S3WebsiteURL**, **SiteBucket**.
{{% /notice %}}

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0006-createcloudformation.png?featherlight=false&width=90pc)

8. In the newly created stack interface

- Select **Outputs**
- Find the value of **VSCodeServerDomainName**.

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0007-createcloudformation.png?featherlight=false&width=90pc)

9. We will use the browser-based **VSCode Server**, which is packed in our Stack, as our development environment.

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0008-createcloudformation.png?featherlight=false&width=90pc)

10. Check **Outputs** of the stack

- Access to **S3**
- Select **Buckets**
- Bucket has been created (**http://BUCKET_NAME.s3-website.REGION.amazonaws.com/**)
- The website is static and the link is saved in **workshop-1/cfn-outputs.json**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0009-createcloudformation.png?featherlight=false&width=90pc)

11. Next we check **DynamoDB**

- Access to **DynamoDB**
- New **Table** has been initialized

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/00010-createcloudformation.png?featherlight=false&width=90pc)

12. Check **Load Balancers**

- Access to **EC2**
- Select **Load Balancers**
- Check the result

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/00011-createcloudformation.png?featherlight=false&width=90pc)