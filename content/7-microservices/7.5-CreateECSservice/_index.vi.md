---
title : "Create ECS Service"
weight : 5
chapter : false
pre : " <b> 7.5 </b> "
---

1.  Cũng trong giao diện Task vừa tạo, chúng ta sẽ tạo một ECS service để chạy Task definition vừa tạo.

- Chọn **Deploy**
- Chọn **Create Sevice**

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0001-createecsservice.png?featherlight=false&width=90pc)

2.  Thiết lập môi trường

- Chọn cluster (**Cluster-STACK_NAME**)

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0002-createecsservice.png?featherlight=false&width=90pc)

3.  Thực hiện cấu hình *Deployment**

- **Application type**, mặc định **Service**
- Thực hiện đặt tên **Service name**
- **Desired tasks**, chọn 1

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0003-createecsservice.png?featherlight=false&width=90pc)

4.  Thực hiện cấu hình **Load Balancing**

- Chọn **Application Load Balancer**
- Chọn **Use an existing load balancer**
- Chọn **alb-STACK_NAME**
- Cấu hình **Listener** (**Port**: 8080 và **Protocol**: HTTP)
- Tạo **Target group**, nhập **```microservice-tg```**
- **Health check path**, nhập **/**
- **Health check grace period**, nhập **300**

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0004-createecsservice.png?featherlight=false&width=90pc)

5.  Cấu hình **Network**

- **VPC**, chọn **Mysfits-STACK_NAME**
- **Subnets**, chọn private subnet
- Về **Security group**, chọn **Use an existing security group**
- Ta chọn **Security group** default và đảm bảo inbound cấu hình **HTTP** (cổng 80)
- Chọn **Deploy**

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0005-createecsservice.png?featherlight=false&width=90pc)

6.  Như vậy, chúng ta tạo service deploy thành công.

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0006-createecsservice.png?featherlight=false&width=90pc)

7.  Sau khi Microservice service deploy, chúng ta thực hiện kiểm tra giao diện website và thực hiện test like.

- Chọn **S3WebsiteURL**

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0007-createecsservice.png?featherlight=false&width=90pc)

8.  Chúng ta sử dụng trình duyệt truy cập vào website. Kiểm tra lại **CloudWatch logs** và hiển thị **"Like processed."**

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0008-createecsservice.png?featherlight=false&width=90pc)

9.  Thực hiện bỏ phần endpoint từ monolith bằng cách sử dụng Cloud9.

- Trong monolith folder, mở **mythicalMysfitsService.py** tìm đoạn code sau:

```
# increment the number of likes for the provided mysfit.
@app.route("/mysfits/<mysfit_id>/like", methods=['POST'])
def likeMysfit(mysfit_id):
    serviceResponse = mysfitsTableClient.likeMysfit(mysfit_id)
    process_like_request()
    flaskResponse = Response(serviceResponse)
    flaskResponse.headers["Content-Type"] = "application/json"
    return flaskResponse
```
Bạn có thể xóa hoặc comment code.

![Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0009-createecsservice.png?featherlight=false&width=90pc)

10.  Sau đó, chúng ta thực hiện build monolith image 

```bash
cd ~/environment/amazon-ecs-mythicalmysfits-workshop/workshop-1/app/monolith-service 
docker build -t monolith-service:nolike2 .
```

![Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/00010-createecsservice.png?featherlight=false&width=90pc)

11.  Thực hiện gán tag và push lên monolith ECR repository.

- Chúng ta sử dụng tag: nolike2.

```bash
docker tag monolith-service:nolike2 $MONO_ECR_REPOSITORY_URI:nolike2
docker push $MONO_ECR_REPOSITORY_URI:nolike2
```
<!-- ![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/00011-createecsservice.png?featherlight=false&width=90pc)
 -->
12.  Kiểm tra **monolith repository** trên ECR, ta sẽ thấy image được push với tag là nolike2.
<!-- 
![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/00012-createecsservice.png?featherlight=false&width=90pc) -->

13.  Bây giờ, hãy tạo một Task Definition cuối cùng cho monolith để tham chiếu đến URI Image Container này và  update dịch vụ monolith để sử dụng Task Definition mới và đảm bảo ứng dụng vẫn hoạt động như trước.