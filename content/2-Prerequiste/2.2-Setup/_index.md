---
title : "Setup your environment"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

#### Clone the workshop Repository

1. Open the **environment** folder

  - In the **VSCode** interface, we first open the folder `~/environment` from the top menu:

  ![vscfile](/images/2-Prerequiste/2.2-Setup/a0001-env.png)

  ![vscfile](/images/2-Prerequiste/2.2-Setup/a0002-env.png)

  Click **I trust the author** on the next dialog.

  ![vscfile](/images/2-Prerequiste/2.2-Setup/a0003-env.png)

2. Clone **Mythical Mysfits Workshop Repository**

  - Open the terminal from the top menu:

  ![vscfile](/images/2-Prerequiste/2.2-Setup/a0004-env.png)

  - In the terminal command line interface, run the following command:

  ```bash
  git clone https://github.com/longthg-workshops/amazon-ecs-mythicalmysfits-workshop.git
  ```

  ![Set up](/images/2-Prerequiste/2.2-Setup/0001-setup.png?featherlight=false&width=90pc)

3. After cloning the repository, change the directory's path:

  ```
  cd amazon-ecs-mythicalmysfits-workshop/workshop-1
  ```

  ![Set up](/images/2-Prerequiste/2.2-Setup/0002-setup.png?featherlight=false&width=90pc)

4. We execute the following command line to install the environment to prepare for the lab.

  ```bash
  script/setup
  ```
  - This script will delete unnecessary **Docker images** to free up space.
  - Also populate the **DynamoDB** table with original data.
  - Upload web content to **S3**.
  - Install some authentication mechanisms related to **Docker**.

  ```bash
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

  When you see **"Success!"** on the interface, the command has been executed successfully.

  ![Set up](/images/2-Prerequiste/2.2-Setup/0004-setup.png?featherlight=false&width=90pc)

5. Check the **S3** interface

- In the bucket where we've just uploaded the website files

![Set up](/images/2-Prerequiste/2.2-Setup/0005-setup.png?featherlight=false&width=90pc)

6. Have a look at the **DynamoDB** interface

- The original data has been filled in **Table** DynamoDB

![Set up](/images/2-Prerequiste/2.2-Setup/0006-setup.png?featherlight=false&width=90pc)

7. We should configure **aws cli** with our **current region** as default:

  ```bash
  export ACCOUNT_ID=$(aws sts get-caller-identity --output text --query Account)
  export TOKEN=$(curl -s -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 60")
  export AWS_REGION=$(curl -H "X-aws-ec2-metadata-token: $TOKEN" -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r '.region')

  echo "export ACCOUNT_ID=${ACCOUNT_ID}" >> ~/.bash_profile
  echo "export AWS_REGION=${AWS_REGION}" >> ~/.bash_profile
  aws configure set default.region ${AWS_REGION}
  aws configure get default.region
  ```

  ![Set up](/images/2-Prerequiste/2.2-Setup/0007-setup.png?featherlight=false&width=90pc)