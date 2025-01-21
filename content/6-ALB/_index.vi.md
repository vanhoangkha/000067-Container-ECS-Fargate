---
title : "ALB và ECS Service"
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---

#### Scale the adoption platform monolith with an ALB and an ECS Service

![Scale the adoption platform monolith with an ALB and an ECS Service](/images/1-Introduce/03-arch.png?featherlight=false&width=90pc)

Phương pháp Run Task  đã sử dụng trong phần trước rất tốt để thử nghiệm, nhưng nếu cần chạy nền tảng áp dụng như một quá trình chạy lâu dài. Bạn cần sử dụng **Elastic Load Balancing Appliction Load Balancer (ALB)** để phân phối các yêu cầu đến các container đang chạy của bạn. Ngoài việc cân bằng tải đơn giản, còn tạo ra các khả năng như định tuyến dựa trên đường dẫn đến các dịch vụ khác nhau.

**ECS** giúp duy trì số lượng **desired task** (số container chạy trong thời gian dài) và tích hợp **ALB** (xử lý việc đăng ký / hủy đăng ký container vào ALB)

Dịch vụ ECS và ALB ban đầu đã được CloudFormation tạo. Trong bài lab này, bạn sẽ cập nhật các tài nguyên đó để lưu trữ monolith service được đóng gói. Sau đó, bạn sẽ tạo một service mới từ đầu sau khi phá vỡ monolith.

1. Truy cập vào **CloudFormation**

- Chọn **STACK_NAME**
- Chọn **Stack details**
- Chọn **Outputs**
- Chọn **LoadBalancerDNS**

![Deploy the container using AWS Fargate](/images/6-ALB/0001-alb.png?featherlight=false&width=90pc)

2. Sử dụng trình duyệt truy cập vào **LoadBalancerDNS**

![Deploy the container using AWS Fargate](/images/6-ALB/0002-alb.png?featherlight=false&width=90pc)

3. Truy cập vào **[ECS](https://ap-southeast-1.console.aws.amazon.com/ecs/v2/clusters?region=ap-southeast-1)**

- Chọn **Clusters**
- Chọn **Cluster-STACK_NAME**

![Deploy the container using AWS Fargate](/images/6-ALB/0003-alb.png?featherlight=false&width=90pc)

4. Trong giao diện **Cluster-STACK_NAME**, chúng ta tiến hành cập nhật **service**

- Chọn **Services**
- Nhấn vào **Update**

![Deploy the container using AWS Fargate](/images/6-ALB/0004-alb.png?featherlight=false&width=90pc)

5. Trong giao diện cập nhật service

- Chọn **Revision** mới nhất
- Chọn **Update**

![Deploy the container using AWS Fargate](/images/6-ALB/0005-alb.png?featherlight=false&width=90pc)

6. Update service thành công.

![Deploy the container using AWS Fargate](/images/6-ALB/0006-alb.png?featherlight=false&width=90pc)

7. Trong giao diện **Cluster-STACK_NAME**

- Chọn **Task**
- Kiểm tra **Monolith-Definition-STACK_NAME** đã được cập nhật **Revision 2**

![Deploy the container using AWS Fargate](/images/6-ALB/0007-alb.png?featherlight=false&width=90pc)

8. Truy  cập vào **CloudFormation**

- Chọn **STACK_NAME**
- Chọn **Stack details**
- Chọn **Outputs**
- Chọn **S3WebsiteURL**

![Deploy the container using AWS Fargate](/images/6-ALB/0008-alb.png?featherlight=false&width=90pc)

9. Sử dụng trình duyệt để truy cập vào **S3WebsiteURL**

![Deploy the container using AWS Fargate](/images/6-ALB/0009-alb.png?featherlight=false&width=90pc)

10. Thực hiện các thao tác trải nghiệm giao diện người dùng

![Deploy the container using AWS Fargate](/images/6-ALB/00010-alb.png?featherlight=false&width=90pc)

11. Truy cập vào **ECS**

- Chọn **Cluster**
- Chọn **Cluster-STACK_NAME**
- Chọn **Tasks**
- Chọn **Monolith-Definition-STACK_NAME** revision 2

![Deploy the container using AWS Fargate](/images/6-ALB/00011-alb.png?featherlight=false&width=90pc)

12. Chọn **Logs**

![Deploy the container using AWS Fargate](/images/6-ALB/00012-alb.png?featherlight=false&width=90pc)

13.  Kiểm tra logs để đảm bảo monolith có thể đọc và ghi **DynamoDB** và có thể xử lý like.

![Deploy the container using AWS Fargate](/images/6-ALB/00013-alb.png?featherlight=false&width=90pc)

14. Kiểm tra CloudWatch logs từ ECS để đảm bảo **Like processed**

![Deploy the container using AWS Fargate](/images/6-ALB/00014-alb.png?featherlight=false&width=90pc)

15. Truy cập **CloudWatch**

- Chọn **Log groups**
- Quan sát log event

![Deploy the container using AWS Fargate](/images/6-ALB/00015-alb.png?featherlight=false&width=90pc)

16. Để phân biệt giữa **service** và task. Ta có thể thực hiện các bước sau: 

- Chọn dịch vụ với **Revision** mới nhất
- Chọn **Update**

![Deploy the container using AWS Fargate](/images/6-ALB/00018-alb.png?featherlight=false&width=90pc)

17. Nâng số **Desired task** lên là 3 và update.

![Deploy the container using AWS Fargate](/images/6-ALB/00016-alb.png?featherlight=false&width=90pc)

18. Sau khi update thành công. 

- Chọn **Task** sẽ thấy 3 task đang chạy.
- Từ đó, ta thấy **ECS services** là khái niệm trong đó ECS cho phép chạy và duy trì một số lượng container cụ thể của các task definition trong một ECS cluster. Một service gồm nhiều task và được duy trì.

![Deploy the container using AWS Fargate](/images/6-ALB/00017-alb.png?featherlight=false&width=90pc)






