---
title : "Containerize the Mythical Mysfits monolith"
weight : 2 
chapter : false
pre : " <b> 4.2 </b> "
---

#### Containerize the Mythical Mysfits monolith

![Containerize monolith](/images/1-Introduce/01-arch.png?featherlight=false&width=90pc)

#### Ý nghĩa của một số INSTRUCTION trong Dockerfile.

- **FROM:** Dùng để chỉ ra image được build từ image gốc nào. Tùy vào mỗi ứng dụng cần đóng gói mà chúng ta sẽ sử dụng image gốc khác nhau.
- **RUN:** Dùng để chạy một lệnh nào đó khi build image.
- **WORKDIR**: Dùng để thiết lập thư mục làm việc. Mọi chỉ thị RUN, CMD, ENTRYPOINT, COPY và ADD sau đó đều sẽ diễn ra bên trong thư mục WORKDIR này.
- **COPY**: COPY thư mục nguồn từ máy host vào filesystem của image.
- **CMD**: Dùng để cung cấp câu lệnh mặc định sẽ được chạy khi Docker Container khởi động từ Image đã build, chỉ có thể có duy nhất 1 chỉ thị CMD. 

1. Kiểm tra **Dockerfile.draft**

```dockerfile
FROM ubuntu:20.04
RUN apt-get update -y
RUN apt-get install -y python3-pip python-dev build-essential
RUN pip3 install --upgrade pip
#[TODO]: Copy python source files and requirements file into container image

#[TODO]: Install dependencies listed in the requirements.txt file using pip3

#[TODO]: Specify a listening port for the container

#[TODO]: Run mythicalMysfitsService.py as the final step. We want this container to run as an executable. Looking at ENTRYPOINT and CMD for this?
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0001-monolith.png?featherlight=false&width=90pc)

2. Hoàn thành Dockerfile

```dockerfile
FROM ubuntu:20.04
RUN apt-get update -y
RUN apt-get install -y python3-pip python-dev build-essential
RUN pip3 install --upgrade pip
#[TODO]: Copy python source files and requirements file into container image
COPY ./service /MythicalMysfitsService
WORKDIR /MythicalMysfitsService
#[TODO]: Install dependencies listed in the requirements.txt file using pip3
RUN pip3 install -r ./requirements.txt
#[TODO]: Specify a listening port for the container
EXPOSE 80
#[TODO]: Run the mythicalMysfitsService.py as the final step
ENTRYPOINT ["python3"]
CMD ["mythicalMysfitsService.py"]
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0002-monolith.png?featherlight=false&width=90pc)

3. Nếu Dockerfile hoàn thành, hãy đổi tên tệp của bạn từ "Dockerfile.draft" thành "Dockerfile" và tiếp tục bước tiếp theo.

```bash
cd ~/environment/amazon-ecs-mythicalmysfits-workshop/workshop-1/app/monolith-service/
mv Dockerfile.draft Dockerfile
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0003-monolith.png?featherlight=false&width=90pc)

4. Thực hiện build image bằng lệnh **docker build [OPTIONS] PATH | URL | -** .

{{% notice note %}}
Lệnh này cần được chạy trong cùng thư mục chứa Dockerfile của bạn. 
{{% /notice %}}

- Lưu ý khoảng thời gian sau đó cho lệnh xây dựng tìm trong thư mục hiện tại cho Dockerfile.

```bash
docker build -t monolith-service .
```


![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0004-monolith.png?featherlight=false&width=90pc)

5. Bạn sẽ thấy một loạt kết quả khi Docker build tất cả các layer của image. 

{{% notice warning %}}
Nếu có sự cố xảy ra trong quá trình build, quá trình build sẽ không thành công và dừng lại (**văn bản màu đỏ và các cảnh báo trên đường đi cũng được miễn là quá trình build không bị lỗi**). 
{{% /notice %}}

```bash
Removing intermediate container a71540b615b4
 ---> 5ab93ce927c8
Step 8/10 : EXPOSE 80
 ---> Running in 27074f1d4c3a
Removing intermediate container 27074f1d4c3a
 ---> f528fe7756d5
Step 9/10 : ENTRYPOINT ["python3"]
 ---> Running in 8ef1757aadb0
Removing intermediate container 8ef1757aadb0
 ---> a1d1ed159fb2
Step 10/10 : CMD ["mythicalMysfitsService.py"]
 ---> Running in da0c544e601b
Removing intermediate container da0c544e601b
 ---> b283e0821fc9
Successfully built b283e0821fc9
Successfully tagged monolith-service:latest
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0005-monolith.png?featherlight=false&width=90pc)

6. Dockerfile của bạn đã được tạo thành công, nhưng chưa tối ưu hóa Dockefile cho microservices. 

{{% notice info %}} 
Vì bạn chuyển monolith thành các microservices, bạn sẽ chỉnh sửa source code (ví dụ **mythicalMysfitsService.py**) và build image này một vài lần. 
{{% /notice %}}

- Kiểm tra Dockerfile

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0006-monolith.png?featherlight=false&width=90pc)

7. Thực hiện tối ưu Dockerfile

```dockerfile
FROM ubuntu:20.04
RUN apt-get update -y
RUN apt-get install -y python3-pip python-dev build-essential
RUN pip3 install --upgrade pip
COPY ./service/requirements.txt .
RUN pip3 install -r ./requirements.txt
COPY ./service /MythicalMysfitsService
WORKDIR /MythicalMysfitsService
EXPOSE 80
ENTRYPOINT ["python3"]
CMD ["mythicalMysfitsService.py"]
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0007-monolith.png?featherlight=false&width=90pc)

8. Để thấy được lợi ích của việc tối ưu hóa Dockerfile, trước tiên bạn cần phải **rebuild monolith image** bằng cách sử dụng Dockerfile mới. 

```bash
docker build -t monolith-service .
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0008-monolith.png?featherlight=false&width=90pc)

9. Sau đó, chúng ta thực hiện thay đổi **mythicalMysfitsService.py** bằng cách thêm 1 câu bình luận ở cuối file.

```python
# This is a comment to force a Docker-rebuild
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/0009-monolith.png?featherlight=false&width=90pc)

10. Docker đã lưu vào bộ nhớ cache các yêu cầu trong lần build lại đầu tiên sau khi sắp xếp lại.

```bash
docker build -t monolith-service .
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00010-monolith.png?featherlight=false&width=90pc)

11. Thực hiện rebuild monolith image một lần nữa. Tham chiếu bộ nhớ cache trong lần build lại thứ hai này
![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00011-monolith.png?featherlight=false&width=90pc)

12. Sử dụng **docker images [OPTIONS] [REPOSITORY[:TAG]]** để liệt kê danh sách image

```bash
docker images
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00012-monolith.png?featherlight=false&width=90pc)

13. Chạy container và kiểm tra

```bash
export TABLE_NAME="$(jq < ~/environment/amazon-ecs-mythicalmysfits-workshop/workshop-1/cfn-output.json -r '.DynamoTable')"
docker run -p 8000:80 -e AWS_DEFAULT_REGION=$AWS_REGION -e DDB_TABLE_NAME=$TABLE_NAME monolith-service
```

{{% notice note %}}
Lưu ý: Bạn có thể tìm thấy tên bảng DynamoDB của mình trong tệp **workshop-1/cfn-output.json** có nguồn gốc từ kết quả đầu ra của CloudFormation Stack
{{% /notice %}}


![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00013-monolith.png?featherlight=false&width=90pc)

14.   Để kiểm tra chức năng cơ bản của dịch vụ monolith, hãy truy vấn dịch vụ bằng tiện ích như **[cURL](https://curl.se/)** đi kèm với bản phân phối linux.

```bash
curl http://localhost:8000/mysfits
```

- Bạn sẽ thấy một mảng JSON với dữ liệu về **Mythical Mysfits**

{{% notice note %}} 
Lưu ý: Các quy trình chạy bên trong vùng chứa Docker có thể xác thực bằng DynamoDB vì chúng có thể truy cập điểm cuối API siêu dữ liệu EC2 đang chạy tại 169.254.169.254 để truy xuất thông tin đăng nhập cho hồ sơ cá thể đã được đính kèm với môi trường Cloud9 của chúng tôi trong tập lệnh thiết lập ban đầu. Các quy trình trong vùng chứa không thể truy cập tệp **~/.aws/credentials**  trong hệ thống tệp máy chủ (trừ khi nó được gắn vào vùng chứa một cách rõ ràng).
{{% /notice %}}


![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00014-monolith.png?featherlight=false&width=90pc)

15.  Quay trợ lại tab chạy monolith container

- Monolith container chạy trên nền trước với tính năng stdout/stderr in ra màn hình, khi nhận được request, sẽ hiện thị **200 "OK"**

```bash
 * Serving Flask app "mythicalMysfitsService" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://0.0.0.0:80/ (Press CTRL+C to quit)
172.17.0.1 - - [26/May/2022 16:49:43] "GET /mysfits HTTP/1.1" 200 -
INFO:werkzeug:172.17.0.1 - - [26/May/2022 16:49:43] "GET /mysfits HTTP/1.1" 200 -
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00015-monolith.png?featherlight=false&width=90pc)

16. Trong tab chạy monolith container, sử dụng tổ hợp phím **Ctrl + C** để dừng chạy container.

{{% notice note %}}
Lưu ý: Container chạy ở foreground với tính năng stdout / stderr in vào bảng điều khiển. Trong môi trường production, khi chạy container trong background và phải cấu hình điểm đến của logs. Chúng ta có thể chạy container trong background (chạy ngầm) bằng cách sử dụng **-d**. 
{{% /notice %}}


```bash
export TABLE_NAME="$(jq < ~/environment/amazon-ecs-mythicalmysfits-workshop/workshop-1/cfn-output.json -r '.DynamoTable')"
docker run -d -p 8000:80 -e AWS_DEFAULT_REGION=$AWS_REGION -e DDB_TABLE_NAME=$TABLE_NAME monolith-service
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00016-monolith.png?featherlight=false&width=90pc)

17.  Liệt kê danh sách docker container để kiểm tra container đang chạy

```bash
docker ps
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00017-monolith.png?featherlight=false&width=90pc)

18. Xem monolith đang chạy trong danh sách (lưu trữ Container ID để sử dụng docker logs). Lặp lại lệnh **curl**, sau đó thực hiện kiểm tra logs

```bash
docker logs <CONTAINER_ID>
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00018-monolith.png?featherlight=false&width=90pc)

19. Hiện tại, chúng ta đang có **Docker image** đang hoạt động, ta thực hiện gán tag và push vào **ECR**. **AWS ECR** là một dịch vụ Docker container registry quản lý hoàn toàn bởi AWS nhằm đơn giản hóa việc lưu trữ, quản lý và triển khai các Docker container image.
**ECR** có thể tích hợp được với **Amazon Elastic Container Service (ECS)** nhằm đơn giản hóa việc thiết lập luồng thực hiện triển khai cho các hệ thống production cũng như loại bỏ đi sự phức tạp trong việc quản lý kho lưu trữ cho các container image. Trong kế tiếp, ta sử dụng ECS pull image từ ECR.

- Truy cập vào ECS và chọn **Repositories**
- Chúng ta sẽ có 2 repository: **STACK_NAME-mono-xxx và STACK_NAME-like-xxx**
- Chọn vào icon sao chép **URL** của **Mono** repository( sử dụng trong các bước tiếp)

{{% notice note %}}
 Note: repository URI  là duy nhất
{{% /notice %}}

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00019-monolith.png?featherlight=false&width=90pc)

20.  Thực hiện gán tag và push container image và monolith repository

```bash
MONO_ECR_REPOSITORY_URI=$(aws ecr describe-repositories | jq -r .repositories[].repositoryUri | grep mono)
docker tag monolith-service:latest $MONO_ECR_REPOSITORY_URI:latest
docker push $MONO_ECR_REPOSITORY_URI:latest
```

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00020-monolith.png?featherlight=false&width=90pc)

21. Truy cập vào trang **ECR repository**, đã xuất hiện image được upload và được gắn thẻ **latest**.

![Containerize the Mythical Mysfits monolith](/images/4-Monolith/4.2-MythicalMysfitsmonolith/00021-monolith.png?featherlight=false&width=90pc)

