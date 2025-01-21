---
title : "Sử dụng AWS Fargate triển khai container"
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

#### Deploy the container using AWS Fargate

![Deploy the container using AWS Fargate](/images/1-Introduce/02-arch.png?featherlight=false&width=90pc)

1. Bước đầu, chúng ta sẽ tạo **Task definitions** để chạy monolith

- Truy cập **[ECS](https://ap-southeast-1.console.aws.amazon.com/ecs/v2/task-definitions?region=ap-southeast-1)**
- Chọn **Task definitions**
- Tìm Task definition có tên **Monolith-Definition-STACK_NAME**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0001-awsfargate.png?featherlight=false&width=90pc)

2. Truy cập vào **[ECR](https://ap-southeast-1.console.aws.amazon.com/ecr/repositories?region=ap-southeast-1)**

- Sao chép **Image URI**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0002-awsfargate.png?featherlight=false&width=90pc)

3. Quay lại giao diện **[ECS](https://ap-southeast-1.console.aws.amazon.com/ecs/v2/task-definitions?region=ap-southeast-1)**

- Chọn **Monolith-Definition-STACK_NAME**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0003-awsfargate.png?featherlight=false&width=90pc)

4. Trong giao diện **Monolith-Definition-STACK_NAME** revision 1. Chúng ta sẽ thực hiện tạo một revision mới.

- Chọn **Create new revision**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0004-awsfargate.png?featherlight=false&width=90pc)

5. Chọn hệ điều hành, lượng bộ nhớ và CPU

    ![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0006-awsfargate.png?featherlight=false&width=90pc)

6. Tiến hành cấu hình **Container**

    - **Name**, nhập tên service mà bạn chọn(Trong bài lab, nhập **```monolith-service```**)
    - Dán **Image URI** đã sao chép vào **Image URI**

    ![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0005-awsfargate.png?featherlight=false&width=90pc)

7. Cấu hình **Log collection**

    - Tìm tên log group của lab trong CloudFormation stack, sao chép physical ID và dán vào giá trị của khóa `awslogs-group`

    ![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0006-awsfargate-2.png?featherlight=false&width=90pc)

8. Hoàn thành tạo new revision

    ![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0007-awsfargate.png?featherlight=false&width=90pc)

9. Trong giao diện điều khiển **Monolith-Definition-STACK_NAME**:

- Chọn **Deploy**
- Chọn **Run stask**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0008-awsfargate.png?featherlight=false&width=90pc)

10. Trong giao diện **Deploy**

- **Environment**, chọn **Existing cluster**, chọn **Cluster-STACK_NAME**
- Chọn **Launch type**
- Trong **Launch type**, chọn **FARGATE**
- **Platform version** chọn **LATEST**
 
![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/0009-awsfargate.png?featherlight=false&width=90pc)

11. Trong phần **Deployment configuration**

- Chọn **Task**
- **Desired** chọn 1

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00010-awsfargate.png?featherlight=false&width=90pc)

12. Tiến hành cấu hình mạng ở mục **Networking**

- **VPC**, chọn **Mysfits-VPC-STACK_NAME**
- **Subnets** chọn **Mysfits-PublicOne-STACK_NAME**
- Chọn **Security Group**, Chọn **Use an existing security group**
- **Security group name**, chọn **default** nhưng phải cấu hình **inbound**  cổng 80
- **Auto-assign public IP** - "ENABLED"
- Chọn **Deploy**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00011-awsfargate.png?featherlight=false&width=90pc)

13. Tạo task thành công

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00012-awsfargate.png?featherlight=false&width=90pc)

14.  Chọn task vừa tạo và chọn **Networking**. 

- Mục đích sử dụng **Public IP** để sử dụng lệnh **curl** kiểm tra bằng cách thực hiện **GET request**.
-  Khi sử dụng kiểu khởi tạo **Fargate**, mỗi task sẽ nhận **ENI** và **Public IP** và **Private IP** của riêng nó. 

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00013-awsfargate.png?featherlight=false&width=90pc)

15. Thực hiện truy cập bằng trình duyệt

```
http://TASK_PUBLIC_IP_ADDRESS/mysfits
```

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00014-awsfargate.png?featherlight=false&width=90pc)

16. Thực hiện lệnh **curl** trên giao diện dòng lệnh của IDE

```
curl http://TASK_PUBLIC_IP_ADDRESS/mysfits
```


![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00015-awsfargate.png?featherlight=false&width=90pc)

17.  Chọn task vừa tạo và chọn **Logs**
    
![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00016-awsfargate.png?featherlight=false&width=90pc)

18. Sử dụng AWS CloudWatch để xem **Log events**

    - Mở [CloudWatch Console](https://console.aws.amazon.com/cloudwatch/home)

    - Chọn **monolith log group** (**STACK_NAME-MythicalMonolithLogGroup-XXX**)

    ![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00017-awsfargate.png?featherlight=false&width=90pc)

    - Chọn một log stream để xem chi tiết các sự kiện được log

    ![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00017a-awsfargate.png?featherlight=false&width=90pc)

    ![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00017b-awsfargate.png?featherlight=false&width=90pc)

19. Sau khi chạy lệnh **curl** thành công ta có thể xóa task

- Chọn **Task**
- Chọn **Monolith-Definition-STACK_NAME** revision 2.
- Chọn **Stop**
- Chọn **Stop selected**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00018-awsfargate.png?featherlight=false&width=90pc)

20. Nếu được hỏi, gõ **Stop** để xác nhận và nhấn nút **Stop**

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00019-awsfargate.png?featherlight=false&width=90pc)

21. Xóa task thành công.  

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00020-awsfargate.png?featherlight=false&width=90pc)

22. Xóa quy tắc cho phép HTTP cổng 80 bạn vừa tạo cho Security Group mặc định của VPC trong stack của lab này.

![Deploy the container using AWS Fargate](/images/5-AmazonECSandAWSFargate/00021-awsfargate.png?featherlight=false&width=90pc)