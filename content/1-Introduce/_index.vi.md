---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

#### Tổng quan

Docker là nền tảng phần mềm cho phép bạn dựng, kiểm thử và triển khai ứng dụng một cách nhanh chóng. Docker đóng gói phần mềm vào các đơn vị tiêu chuẩn hóa được gọi là container có mọi thứ mà phần mềm cần để chạy, trong đó có thư viện, công cụ hệ thống, mã và thời gian chạy. Bằng cách sử dụng Docker, bạn có thể nhanh chóng triển khai và thay đổi quy mô ứng dụng vào bất kỳ môi trường nào và biết chắc rằng mã của bạn sẽ chạy được.
Việc chạy Docker trên AWS đem đến cho các nhà phát triển và quản trị viên một phương thức dựng, vận chuyển và chạy ứng dụng phân phối ở quy mô bất kỳ có chi phí thấp và độ tin cậy cao.

{{% notice info %}}
Docker hợp tác với AWS để hỗ trợ các nhà phát triển nhanh chóng đưa ứng dụng hiện đại lên đám mây. Sự hợp tác này giúp nhà phát triển sử dụng Docker Compose và Docker Desktop để tận dụng cùng một quy trình làm việc cục bộ mà họ sử dụng ngày nay để triển khai các ứng dụng trên Amazon ECS và AWS Fargate một cách liền mạch.
{{% /notice %}}

#### Cách thức hoạt động của Docker

Docker hoạt động bằng cách cung cấp phương thức tiêu chuẩn để chạy mã của bạn. Docker là hệ điều hành dành cho container. Cũng tương tự như cách máy ảo ảo hóa (loại bỏ nhu cầu quản lý trực tiếp) phần cứng máy chủ, các container sẽ ảo hóa hệ điều hành của máy chủ. Docker được cài đặt trên từng máy chủ và cung cấp các lệnh đơn giản mà bạn có thể sử dụng để dựng, khởi động hoặc dừng container.

Các dịch vụ AWS như **AWS Fargate, Amazon ECS, Amazon EKS và AWS Batch** giúp bạn dễ dàng chạy các container Docker ở quy mô lớn.


![Docker basic](/images/1-Introduce/0001-docker.png?featherlight=false&width=60pc)

Trong bài lab, chúng ta sẽ thực hiện chuyển **Monolith** sang **Microservices** với **Docker** và **AWS Fargate**