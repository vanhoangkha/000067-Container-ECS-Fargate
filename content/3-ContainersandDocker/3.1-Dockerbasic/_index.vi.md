---
title : "Những điều cơ bản về Docker"
weight : 1 
chapter : false
pre : " <b> 3.1 </b> "
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


Trong bài lab, chúng ta thực hiện các lệnh cơ bản Docker với **AWS Cloud9**

1. Kiểm tra client và server đang hoạt động bằng lệnh:

```bash
docker --version
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0001-dockerbasic.png?featherlight=false&width=90pc)

2. **Docker container** được xây dựng từ **image**.

- Lệnh pull

```bash
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```

-  Trước hết, chúng ta sử dụng lệnh **docker pull nginx\:latest** để kéo **nginx image** mới nhất từ **Docker Hub**.

```bash
docker pull nginx\:latest
```
 
![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0002-dockerbasic.png?featherlight=false&width=90pc)

3. Để kiểm tra kéo image về thành công(**image sẽ nằm trong local machine Docker cache**). 

- Usage

```bash
docker images [OPTIONS] [REPOSITORY[:TAG]]
```

- Mục đích liệt kê danh sách các image.

```bash
docker images
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0003-dockerbasic.png?featherlight=false&width=90pc)

4. **Docker Daemon** đóng vai trò **server**, nhận các **RESTful requests** từ **Docker Client** và thực thi. 

- Chúng ta sử dụng lệnh **docker run -d -p 8081:80 --name nginx nginx\:latest**.

```bash
docker run -d -p 8081:80 --name nginx nginx\:latest
```

- **-d**: Chạy container ở chế độ ngầm
- Đặt tên cho container là **nginx**
- **-p 8081:80**: Expose cổng 80 của container ra cổng 8081 của máy **host**
- **nginx:latest**: Container được khởi chạy từ image là **nginx:latest**

- Lệnh tham khảo để chạy một container:

```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0004-dockerbasic.png?featherlight=false&width=90pc)

5. Kiểm tra các **container nginx** đang chạy bằng lệnh:

```bash
docker ps
```

- Để thực hiện liệt kê các container ta thực hiện lệnh:

```bash
docker ps [OPTIONS]
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0005-dockerbasic.png?featherlight=false&width=90pc)

6. Sử dụng lệnh **curl http://localhost:8081** để sử dụng **nginx container** và xác thực nó đang hoạt động với **index.html**

```bash
curl http://localhost:8081
```

- Mẫu lệnh **curl** có dạng sau:

```bash
curl [options/URLs]
```

{{% notice info %}}
Ngoài ra bạn có thể đọc thêm về **[CURL](https://curl.se/)**
{{% /notice %}}


![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0006-dockerbasic.png?featherlight=false&width=90pc)

7. Để xem nhật ký của **nginx và container**. 

- Chúng ta sử dụng lệnh **docker logs nginx**. Xuất hiện sự kiện **curl request**

```bash
docker logs nginx
```

- Tham khảo lệnh tìm nạp nhật ký của container:

```bash
 docker logs [OPTIONS] CONTAINER
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0007-dockerbasic.png?featherlight=false&width=90pc)

8. Tiếp đến, thực hiện lệnh **docker exec -it nginx /bin/bash** để tương tác với **container filesystem và constraints**

```bash
docker exec -it nginx /bin/bash
```

- Tham khảo lệnh tương tác trong container đang chạy:

```bash
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0008-dockerbasic.png?featherlight=false&width=90pc)

9. Chúng ta thực hiện xem nội dung của nginx bằng lệnh:

```bash
cd /usr/share/nginx/html
cat index.html
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/0009-dockerbasic.png?featherlight=false&width=90pc)

10. Sử dụng **exit** để thoát khỏi

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/00010-dockerbasic.png?featherlight=false&width=90pc)

11. Để dừng chạy container chúng ta thực hiện lệnh

```bash
docker stop nginx
```

- Tham khảo lệnh dừng một hoặc nhiều container:

```bash
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/00011-dockerbasic.png?featherlight=false&width=90pc)

12. Sử dụng **docker ps -a** để xem container (bao gồm container đã dừng) để khởi động lại sử dụng lệnh: **```docker start nginx```**

```bash
docker ps -a
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/00012-dockerbasic.png?featherlight=false&width=90pc)

13. Thực hiện xóa container (đầu vào là container ID hoặc container name)

```bash
docker rm nginx
```

- Tham khảo lệnh xóa một hoặc nhiều container:

```bash
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/00013-dockerbasic.png?featherlight=false&width=90pc)

14. Thực hiện xóa nginx image bằng lệnh (định dạng image được xóa có thể là **name:tag** hoặc **IMAGE ID**)

```bash
docker rmi nginx\:latest
```
- Tham khảo lệnh xóa một hoặc nhiều image:

```bash
 docker rmi [OPTIONS] IMAGE [IMAGE...]
```

![Docker basic](/images/3-ContainersandDocker/3.1-Dockerbasic/00014-dockerbasic.png?featherlight=false&width=90pc)
