---
title : "Tạo Stack CloudFormation"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

#### Tạo Stack CloudFormation

1. Truy cập vào [Deploy to AWS](https://ap-southeast-1.console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create?stackName=mysfits-fargate&templateURL=https://s3.amazonaws.com/mythical-mysfits-website/fargate/core.yml) để tiến hành tạo stack.

{{% notice note %}} 
Ngoài ra, bạn cũng có thể tạo Stack CloudFormation với bằng cách Upload [file yaml](https://s3.amazonaws.com/mythical-mysfits-website/fargate/core.yml)
{{% /notice %}}

- Bước đầu tiên, cấu hình template. Chọn **Template is ready**
- **Template source**, chọn **Amazon S3 URL**
- Trong bài lab, đã cấu hình sẵn **Amazon S3 URL** 
- Chọn **Next**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0001-createcloudformation.png?featherlight=false&width=90pc)

2. Chúng ta cấu hình chi tiết stack

- **Stack name**, nhập tên stack mà bạn muốn đặt.

{{% notice tip %}}
**STACK_NAME** sẽ được sử dụng làm mào đầu hoặc mào cuối của tên của các dịch vụ trong bài lab này. Ví dụ: **alb-STACK_NAME-XXX**
{{% /notice %}}
- Trong phần **Parameters**, chọn **false** cho **SkipBucket**
- Chọn **Next**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0002-createcloudformation.png?featherlight=false&width=90pc)

3. Tiến hành **Configure stack options**

- **Tags**, nhập giá trị **key-value** (*bạn nhập tùy ý*)

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0003-createcloudformation.png?featherlight=false&width=90pc)

4. Chọn **Next**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0004-createcloudformation.png?featherlight=false&width=90pc)

5. Kiểm tra lại cấu hình **stack**

- Chọn **I acknowledge that AWS CloudFormation might create IAM resources**
- Chọn **Create Stack**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0005-createcloudformation.png?featherlight=false&width=90pc)

6. Quá trình tạo stack trong khoảng **7 phút**. 

- Chọn **stack** tạo thành công
- Chọn **Events**
- Xem quá trình tạo stack

{{% notice info %}}
Stack này khởi tạo **Cloud9 Environment**, **DynamoDB Table**, **LoadBalancerDNS**, **ProfileName**, **S3WebsiteURL**, **SiteBucket**.
{{% /notice %}}

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0006-createcloudformation.png?featherlight=false&width=90pc)

7. Trong giao diện stack vừa tạo

- Chọn **Outputs**
- Chọn **value** là đường dẫn **Cloud9** của **Key** Cloud9Env. 


![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0007-createcloudformation.png?featherlight=false&width=90pc)

8. Chúng ta sử dụng **AWS Cloud9** làm môi trường phát triển.

{{% notice note %}}
Chúng ta sẽ sử dụng **Cloud9 Environment** này trong suốt cả bài lab. Môi trường **AWS Cloud9 do CloudFormation** có tên là **Project- STACK_NAME**
{{% /notice %}}

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0008-createcloudformation.png?featherlight=false&width=90pc)

9. Kiểm tra **Outputs** của stack

- Truy cập vào **S3**
- Chọn **Buckets**
- Bucket đã được tạo (**http://BUCKET_NAME.s3-website.REGION.amazonaws.com/**)
- Trang web tĩnh và được lưu đường dẫn trong **workshop-1/cfn-outputs.json**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0009-createcloudformation.png?featherlight=false&width=90pc)

10. Tiếp theo chúng kiểm tra **DynamoDB**

- Truy cập vào **DynamoDB**
- **Table** mới đã được khởi tạo

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/00010-createcloudformation.png?featherlight=false&width=90pc)

11. Kiểm tra **Load Balancers**

- Truy cập vào **EC2**
- Chọn **Load Balancers**
- Kiểm tra kết quả

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/00011-createcloudformation.png?featherlight=false&width=90pc)

