---
title : "Thiết lập môi trường"
weight : 2 
chapter : false
pre : " <b> 2.2 </b> "
---

#### Thiết lập môi trường


1. Open the **environment** folder

  - Trong giao diện web của **VSCode**, đầu tiên ta mở thư mục `~/environment` qua menu:

  ![vscfile](/images/2-Prerequiste/2.2-Setup/a0001-env.png)

  ![vscfile](/images/2-Prerequiste/2.2-Setup/a0002-env.png)

  Nhấn vào **I trust the author** tại hộp thoại tiếp theo.

  ![vscfile](/images/2-Prerequiste/2.2-Setup/a0003-env.png)


2. Tải **Mythical Mysfits Workshop Repository** về môi trường

  - Mở terminal bằng menu hoặc tổ họp phím **Ctrl + Shift + C**

  ![vscfile](/images/2-Prerequiste/2.2-Setup/a0004-env.png)

  - Trong giao diện dòng lệnh, chạy lệnh sau:

  ```bash
  git clone https://github.com/longthg-workshops/amazon-ecs-mythicalmysfits-workshop.git
  ```

  ![Set up](/images/2-Prerequiste/2.2-Setup/0001-setup.png?featherlight=false&width=90pc)

3. Sau khi clone repository, thay đổi đường dẫn của thư mục:

  ```bash
  cd amazon-ecs-mythicalmysfits-workshop/workshop-1
  ```

  ![Set up](/images/2-Prerequiste/2.2-Setup/0002-setup.png?featherlight=false&width=90pc)

3. Chúng ta thực hiện dòng lệnh sau để tiến hành cài đặt môi trường chuẩn bị cho bài lab.

  ```bash
  script/setup
  ```
  - Đoạn script này sẽ xóa đi **Docker images** không cần thiết để giải phóng dung lượng.
  -  Đồng thời điền vào bảng **DynamoDB** dữ liệu gốc.
  -  Tải nội dung web lên **S3**.
  - Cài đặt một số cơ chế xác thực liên quan đến **Docker**. 

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

  echo "Success!"
  ```

  ![Set up](/images/2-Prerequiste/2.2-Setup/0003-setup.png?featherlight=false&width=90pc)

4. Khi bạn thấy trên giao diện hiển thị **"Success!"** là thực thi lệnh thành công.

  ![Set up](/images/2-Prerequiste/2.2-Setup/0004-setup.png?featherlight=false&width=90pc)

5. Kiểm tra trong giao diện **S3**

  - Trong bucket đã được upload các tệp website

  ![Set up](/images/2-Prerequiste/2.2-Setup/0005-setup.png?featherlight=false&width=90pc)

6. Kiểm tra trong giao diện **DynamoDB**

- Dữ liệu gốc đã được điền vào **Table** DynamoDB

![Set up](/images/2-Prerequiste/2.2-Setup/0006-setup.png?featherlight=false&width=90pc)

7. Chúng ta nên cấu hình **aws cli**  với **current region** của chúng ta làm mặc định:

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

