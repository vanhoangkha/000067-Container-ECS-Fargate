---
title : "Clone Repository"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

#### Clone Repository

1. Clone **Mythical Mysfits Workshop Repository**

- In the **Cloud9 IDE** interface, we use the following command to clone the repository:

```
git clone https://github.com/aws-samples/amazon-ecs-mythicalmysfits-workshop.git
```

![Set up](/images/2-Prerequiste/2.2-Setup/0001-setup.png?featherlight=false&width=90pc)

2. After cloning the repository, change the directory's path:

```
cd amazon-ecs-mythicalmysfits-workshop/workshop-1
```

![Set up](/images/2-Prerequiste/2.2-Setup/0002-setup.png?featherlight=false&width=90pc)

3. We execute the following command line to install the environment to prepare for the lab.

```
script/setup
```
- This script will delete unnecessary **Docker images** to free up space.
- Also populate the **DynamoDB** table with original data.
- Upload web content to **S3**.
- Install some authentication mechanisms related to **Docker**.

```
#! /bin/bash

set -eu

echo "Removing unneeded docker images..."
docker images -q | xargs docker rmi || true

echo "Installing dependencies..."
sudo yum install -y jq

echo "Fetching CloudFormation outputs..."
script/fetch-outputs

echo "Populating DynamoDB table..."
script/load-ddb

echo "Uploading static site to S3..."
if [[ $# -eq 1 ]]; then
  script/upload-site $1
else
  script/upload-site
fi

echo "Installing ECR Cred Helper..."
sudo script/credhelper

echo "Attaching Instance Profile to Cloud9..."
script/associate-profile

echo "Success!"
```


![Set up](/images/2-Prerequiste/2.2-Setup/0003-setup.png?featherlight=false&width=90pc)

4. When you see **"Success!"** on the interface, the command has been executed successfully.

![Set up](/images/2-Prerequiste/2.2-Setup/0004-setup.png?featherlight=false&width=90pc)

5. Check-in **S3** interface

- In the bucket have been uploaded website files

![Set up](/images/2-Prerequiste/2.2-Setup/0005-setup.png?featherlight=false&width=90pc)

6. Test in the **DynamoDB** interface

- The original data has been filled in **Table** DynamoDB

![Set up](/images/2-Prerequiste/2.2-Setup/0006-setup.png?featherlight=false&width=90pc)

7. We should configure **aws cli** with our **current region** as default:

```
export ACCOUNT_ID=$(aws sts get-caller-identity --output text --query Account)
export AWS_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r '.region')

echo "export ACCOUNT_ID=${ACCOUNT_ID}" >> ~/.bash_profile
echo "export AWS_REGION=${AWS_REGION}" >> ~/.bash_profile
aws configure set default.region ${AWS_REGION}
aws configure get default.region
```

![Set up](/images/2-Prerequiste/2.2-Setup/0007-setup.png?featherlight=false&width=90pc)