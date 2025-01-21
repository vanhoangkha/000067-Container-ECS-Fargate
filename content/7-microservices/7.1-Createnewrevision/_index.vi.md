---
title : "Tạo Revision"
weight : 1
chapter : false
pre : " <b> 7.1 </b> "
---

#### Tạo Revision

1. Bước đầu tiên, chúng ta thêm một số glue code trong **monolith** để chuyển **like** function thành một dịch vụ riêng (microservice). Trong bài lab, sử dụng **Cloud9** và tìm **app/monolith-service/service/mythicalMysfitsService.py** file. Sau đó thực hiện bỏ bình luận phần code sau:

```python
# @app.route("/mysfits/<mysfit_id>/fulfill-like", methods=['POST'])
# def fulfillLikeMysfit(mysfit_id):
#     serviceResponse = mysfitsTableClient.likeMysfit(mysfit_id)
#     flaskResponse = Response(serviceResponse)
#     flaskResponse.headers["Content-Type"] = "application/json"
#     return flaskResponse
```

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0001-createrevision.png?featherlight=false&width=90pc)

2. Với tính năng mới được thêm vào **monolith**, chúng ta thực hiện rebuild monolith docker image với tag mới (nolike). 

```bash
 cd ~/environment/amazon-ecs-mythicalmysfits-workshop/workshop-1/app/monolith-service
 MONO_ECR_REPOSITORY_URI=$(aws ecr describe-repositories | jq -r .repositories[].repositoryUri | grep mono)
 docker build -t monolith-service:nolike .
```

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0002-createrevision.png?featherlight=false&width=90pc)

3. Thực hiện **push** monolith docker image lên **ECR**

- Cách tốt nhất là tránh tag latest, có thể không rõ ràng. Thay vào đó, hãy chọn một tag duy nhất , tên mô tả hoặc người dùng tốt hơn là Git SHA và / hoặc ID phiên bản).

```bash
 docker tag monolith-service:nolike $MONO_ECR_REPOSITORY_URI:nolike
 docker push $MONO_ECR_REPOSITORY_URI:nolike
```

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0003-createrevision.png?featherlight=false&width=90pc)

4. Thực hiện kiểm tra monolith docker image đã được push lên ECR chưa?

- Truy cập vào **ECS**
- Chọn **Task Definitions**
- Chọn **Monolith-Definitions-STACK_NAME** (lưu các bạn có thể khác trong hình vì phần sau phụ thuộc vào STACK_NAME mà bạn đặt)

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0004-createrevision.png?featherlight=false&width=90pc)

5. Sau đó, chọn **Monolith-Definition-STACK_NAME** revision 2.

- Chọn **Create new revision**

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0005-createrevision.png?featherlight=false&width=90pc)

6. Truy cập vào **ECR** để xem các repository. Bây giờ, trong phần **Images** đã xuất hiện 2 image với 2 tag là latest và **nolike**. 

- Sao chép **Image URI**

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0006-createrevision.png?featherlight=false&width=90pc)

7. Sử dụng **Image URI** tag **nolike** tạo **New revision**

- Thực hiện cấu hình **Container**
- Thay **Image URI** bằng **Image URI** tag **nolike**

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0007-createrevision.png?featherlight=false&width=90pc)

8. Chọn **Create**

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0008-createrevision.png?featherlight=false&width=90pc)

9. Hoàn thành tạo **Monolith-Definition-STACK_NAME** revision 3.

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0009-createrevision.png?featherlight=false&width=90pc)