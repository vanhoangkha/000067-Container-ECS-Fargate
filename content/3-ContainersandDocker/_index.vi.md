---
title : "Giới thiệu Docker và Container"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---

#### Giới thiệu Docker và Container

Trong phần này, chúng ta sẽ thực hành một số lệnh cơ bản về **Docker** và hiểu khái niệm về **Container**.

#### Chạy Docker trên AWS

AWS cung cấp hỗ trợ cho cả giải pháp mã nguồn mở lẫn thương mại của Docker. Có nhiều cách chạy container trên AWS, trong đó có **Amazon Elastic Container Service (ECS)** là dịch vụ quản lý container có quy mô cực kỳ linh hoạt và hiệu năng cao. Khách hàng có thể dễ dàng triển khai ứng dụng đã đưa vào container của mình từ môi trường Docker cục bộ lên thẳng **Amazon ECS**. 

**AWS Fargate** là công nghệ dành cho **Amazon ECS** cho phép bạn chạy container trong sản xuất mà không cần triển khai hoặc quản lý cơ sở hạ tầng.  **AWS Fargate** là công nghệ dành cho **Amazon ECS** cho phép bạn chạy container mà không cần cung cấp hay quản lý máy chủ. 

**Amazon Elastic Container Registry (ECR)** là kho container riêng bảo mật và có độ sẵn sàng cao giúp việc lưu trữ và quản lý ảnh container Docker của bạn trở nên dễ dàng, mã hóa và nén image khi lưu trữ để quá trình bung diễn ra nhanh chóng và bảo mật. 

#### Nội dung

1. [Docker cơ bản](3.1-dockerbasic/)
2. [Container image](3.2-containerimage/)