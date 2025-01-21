---
title : "Tạo Stack CloudFormation"
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

#### Tạo Stack CloudFormation

1. Sử dụng công cụ [Argon2 Hash Generator](https://www.coderstool.com/argon2-hash-generator) để tạo chuỗi hash cho mật khẩu đăng nhập vào VSCode Server trên trình duyệt.

    - Nhập mật khẩu gốc **(chưa hash)**. Lưu mật khẩu gốc để nhập vào khi đăng nhập VSCode ở các bước sau.
    - Đảm bảo các giá trị sau. Nếu không, mật khẩu của bạn không dùng được:
    
        - Parallelism Factor: 1
        - Memory Cost: 4096
        - Iterations: 3
        - Hash Length: 16
        - Hash Type: Argon2i

2. Truy cập vào bảng điều khiển [CloudFormation](https://console.aws.amazon.com/cloudformation/) để tiến hành tạo stack.

![CFN Console](/images/2-Prerequiste/2.1-CreateCloudFormation/0001-cloudformationmenu.png)

Dùng [file yaml này](/workloads/core.yaml) để triển khai stack của bạn.

- Bước đầu tiên, cấu hình template. Chọn **Template is ready**
- **Template source**, chọn **Amazon S3 URL**
- Trong bài lab, đã cấu hình sẵn **Amazon S3 URL** 
- Nhấn vào **Next**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0001-createcloudformation.png?featherlight=false&width=90pc)

3. Chúng ta cấu hình chi tiết stack

- **Stack name**, nhập tên stack mà bạn muốn đặt.

{{% notice tip %}}
**STACK_NAME** sẽ được sử dụng làm mào đầu hoặc mào cuối của tên của các dịch vụ trong bài lab này. Ví dụ: **alb-STACK_NAME-XXX**
{{% /notice %}}

- Trong phần **Parameters** (các tham số):

    - Với **IdeAmiId**, giá trị mặc định là bản AMI mới nhất của Amazon Linux 2023. Bạn có thể thay đổi thành AMI khác theo mong muốn.

    - Nhập loại EC2 instance tại **instance type**. Để giảm chi phí, bạn có thể để giá trị `t2.micro` (áp dụng cho chương trình miễn phí) hoặc `t3.micro`. Tuy nhiên, để đảm bảo hiệu suất, chúng tôi khuyến khích dùng `t3.small` hoặc kiểu máy lớn hơn
    
    - Chọn **false** đối với **SkipBucket**

    - Với **VSCodeServerVersion**, nhập phiên bản mong muốn (bỏ chữ v ở trước). Bạn có thể xem danh sách các phiên bản tại [đây](https://github.com/coder/code-server/releases).

- Nhấn vào **Next**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0002-createcloudformation.png?featherlight=false&width=90pc)

4. Tiếp tục qua trang **Configure stack options**

    - **Tags**, nhập giá trị **key-value** (*bạn nhập tùy ý*)

    ![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0003-createcloudformation.png?featherlight=false&width=90pc)

    - Nhấn **Next**

    ![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0004-createcloudformation.png?featherlight=false&width=90pc)

    - **Stack failure options** - Chọn cách bạn muốn stack xử lý khi gặp sự cố triển khai.

    ![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0003-createcloudformationbehaviour.png?featherlight=false&width=90pc)

5. Tích hộp kiểm tại **I acknowledge that AWS CloudFormation might create IAM resources**, rồi nhấn **Next**.

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0004-createcloudformation.png?featherlight=false&width=90pc)

6. Kiểm tra cấu hình của **stack**. Khi bạn đã hài lòng, nhấn **Submit**.

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0005-createcloudformation.png?featherlight=false&width=90pc)

7. Quá trình tạo stack trong khoảng **7 phút**. Khi hoàn thành, trạng thái sẽ chuyển thành **CREATE_COMPLETE**. 

{{% notice info %}}
Stack này khởi tạo một **EC2 Instance** được cài sẵn **VSCode IDE**, **DynamoDB Table**, **LoadBalancerDNS**, **ProfileName**, **S3WebsiteURL**, **SiteBucket**.
{{% /notice %}}

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0006-createcloudformation.png?featherlight=false&width=90pc)

8. Trong giao diện stack vừa tạo

- Qua thẻ **Outputs**
- Tìm giá trị của **VSCodeServerDomainName**.

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0007-createcloudformation.png?featherlight=false&width=90pc)

9. Chúng ta sử dụng **VSCode Server** (được tạo trong stack) làm môi trường phát triển.

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0008-createcloudformation.png?featherlight=false&width=90pc)

10. Kiểm tra **Outputs** của stack

- Truy cập vào **S3**
- Chọn **Buckets**
- Bucket đã được tạo (**http://BUCKET_NAME.s3-website.REGION.amazonaws.com/**)
- Trang web tĩnh và được lưu đường dẫn trong **workshop-1/cfn-outputs.json**

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/0009-createcloudformation.png?featherlight=false&width=90pc)

11. Tiếp theo chúng kiểm tra **DynamoDB**

- Truy cập vào **DynamoDB**
- **Table** mới đã được khởi tạo

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/00010-createcloudformation.png?featherlight=false&width=90pc)

12. Kiểm tra **Load Balancers**

- Truy cập vào **EC2**
- Chọn **Load Balancers**
- Kiểm tra kết quả

![Create Stack CloudFormation](/images/2-Prerequiste/2.1-CreateCloudFormation/00011-createcloudformation.png?featherlight=false&width=90pc)

