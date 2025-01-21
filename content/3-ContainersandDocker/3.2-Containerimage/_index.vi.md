---
title : "Container image"
weight : 2 
chapter : false
pre : " <b> 3.2 </b> "
---

#### Cách xây dựng container image

Trong phần này chúng ta thực hiện build container image. Làm việc với Dockerfile.

Dockerfile là một file dạng text không có phần đuôi mở rộng, chứa các đặc tả về một trường thực thi phần mềm, cấu trúc cho Docker Image. Từ những câu lệnh đó, Docker sẽ build ra Docker image (thường có dung lượng nhỏ từ vài MB đến lớn vài GB).

#### Tổng quan về Dockerfile

Cú pháp chung của một **Dockerfile**

```dockerfile
INSTRUCTION arguments
```

- **INSTRUCTION** là tên các chỉ thị có trong **Dockerfile**, mỗi chỉ thị thực hiện một nhiệm vụ nhất định, được Docker quy định. 
- Khi khai báo các chỉ thị này phải được viết bằng chữ **IN HOA**.
- Một **Dockerfile** bắt buộc phải bắt đầu bằng chỉ thị **FROM** để khai báo đâu là image sẽ được sử dụng làm nền để xây dựng nên image của bạn.
- **arguments** là phần nội dung của các chỉ thị, quyết định chỉ thị sẽ làm gì.

#### Một số chỉ thị trong Dockerfile

**FROM**

```dockerfile
FROM <image> [AS <name>]
FROM <image>[:<tag>] [AS <name>]
FROM <image>[@<digest>] [AS <name>]
```

**LABEL**

```dockerfile
LABEL <key>=<value> <key>=<value> <key>=<value> ... <key>=<value> 
```

**MAINTAINER**

```dockerfile
MAINTAINER <name> [<email>]
```

**RUN**

```dockerfile
RUN <command>
```

**ADD**

```dockerfile
ADD [--chown=<user>:<group>] <src>... <dest>
ADD [--chown=<user>:<group>] ["<src>",... "<dest>"]
```
**COPY**

```dockerfile
COPY [--chown=<user>:<group>] <src>... <dest>
COPY [--chown=<user>:<group>] ["<src>",... "<dest>"]
```
**ENV**

```dockerfile
ENV <key>=<value> ...
```

**CMD** Dùng để cung cấp câu lệnh mặc định sẽ được chạy khi Docker Container khởi động từ Image đã build, chỉ có thể có duy nhất 1 chỉ thị CMD.

#### Thực hành

1. Tạo thư mục cho container image

```bash
mkdir ~/environment/container-image
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0001-containerimage.png?featherlight=false&width=90pc)

2. Nhập **cd container-image** để thay đổi vào thư mục đó.

```bash
cd ~/environment/container-image
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0002-containerimage.png?featherlight=false&width=90pc)

3. Chạy **touch Dockerfile** để tạo Dockerfile. Tệp này sẽ chứa một tập hợp các bước cần thiết để xây dựng container image.

```bash
touch Dockerfile
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0003-containerimage.png?featherlight=false&width=90pc)

4. Chạy lệnh dưới đây để cập nhật nội dung Dockerfile

```bash
cat <<EOF > Dockerfile
FROM nginx\:latest
COPY index.html /usr/share/nginx/html
EOF
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0004-containerimage.png?featherlight=false&width=90pc)

5. Chạy **touch index.html** để tạo một tệp html trống sẽ chứa một thông báo đơn giản.

```bash
touch index.html
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0005-containerimage.png?featherlight=false&width=90pc)

6. Sử dụng **echo** để chuyển một thông báo đơn giản vào tệp **index.html**

```bash
echo "We've added our own custom content into the container" >> index.html
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0006-containerimage.png?featherlight=false&width=90pc)

7. Sử dụng **docker build -t nginx:1.0 .** để xây dựng container image nginx từ Dockerfile.

```bash
docker build -t nginx:1.0 .
```

- Tham khảo lệnh build image từ một Dockerfile

```bash
docker build [OPTIONS] PATH | URL | -
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0007-containerimage.png?featherlight=false&width=90pc)

8. Sử dụng **docker history nginx:1.0** để xem tất cả các bước và base container. 

```bash
docker history nginx:1.0
```

- Tham khảo lệnh xem lịch sử của một image:

```bash
docker history [OPTIONS] IMAGE
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0008-containerimage.png?featherlight=false&width=90pc)

9. Sử dụng lệnh **docker run -p 8081:80 --name nginx nginx:1.0** để chạy container ( không sử dụng chế độ chạy ngầm nhằm dễ dàng gỡ lỗi)

```bash
docker run -p 8081:80 --name nginx nginx:1.0
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/0009-containerimage.png?featherlight=false&width=90pc)

10.  Mở một **tab Terminal** khác ( **Window -> New Terminal** ). Chạy **curl http://localhost:8081** trong tab  một vài lần và xem nội dung mới.

```bash
curl http://localhost:8081
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00010-containerimage.png?featherlight=false&width=90pc)

11. Quay lại tab đầu tiên và xem các dòng nhật ký được gửi ngay đến STDOUT. Gõ **Ctrl-C** để thoát khỏi đầu ra nhật ký. Lưu ý rằng container đã được dừng lại nhưng vẫn ở đó khi chạy **docker ps -a**.

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00011-containerimage.png?featherlight=false&width=90pc)

12. Sử dụng **docker ps -a**

```bash
docker ps -a
```
![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00012-containerimage.png?featherlight=false&width=90pc)

13.  Sử dụng **sudo docker inspect nginx** để xem thông tin chi tiết về container đã dừng.

```bash
sudo docker inspect nginx
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00013-containerimage.png?featherlight=false&width=90pc)

14.  Sử dụng **docker rm nginx** để xóa container

```bash
docker rm nginx
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00014-containerimage.png?featherlight=false&width=90pc)

15.  Gắn một số tệp từ máy chủ lưu trữ vào container thay vì nhúng chúng vào image.

```bash
docker run -d -p 8081:80 -v /home/ec2-user/environment/container-image/index.html:/usr/share/nginx/html/index.html\:ro --name nginx nginx\:latest
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00015-containerimage.png?featherlight=false&width=90pc)

16.  Thực hiện **curl http://localhost:8081**. Lưu ý rằng mặc dù đây là upstream nginx image từ Docker Hub nhưng nội dung có ở đó.

```bash
curl http://localhost:8081
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00016-containerimage.png?featherlight=false&width=90pc)

17. Chỉnh sửa tệp index.html

```bash
echo "This is another line I've added to my container" >> index.html
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00017-containerimage.png?featherlight=false&width=90pc)

18. Thử lại **curl http://localhost:8081**

```bash
curl http://localhost:8081
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00018-containerimage.png?featherlight=false&width=90pc)

19. Cuối cùng, chạy **docker stop nginx** và **docker rm nginx** dừng và loại bỏ container

```bash
docker stop nginx && docker rm nginx
```

![Building a container image](/images/3-ContainersandDocker/3.2-Containerimage/00019-containerimage.png?featherlight=false&width=90pc)

