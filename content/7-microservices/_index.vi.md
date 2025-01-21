---
title : "Microservices với AWS Fargate"
weight : 7 
chapter : false
pre : " <b> 7. </b> "
---

#### Microservices với AWS Fargate

Trong lab này, chúng ta sẽ thực hiện phá vỡ monolith chuyển thành các microservice. 

Monolith cung cấp tài nguyên API khác nhau trên các định tuyến khác để tìm nạp thông tin về **Mysfits**, trải nghiệm **like** hoặc **adopt**

Logic của các tài nguyên này bao gồm một số **proccess** (như đảm bảo rằng người dùng được phép thực hiện một hành động cụ thể, rằng Mysfit đủ điều kiện để áp dụng, v.v.) và thực hiện một số tương tác với **persistence layer** (cụ thể là DynamoDB).

Thay vì sử dụng nhiều service khác nhau tương tác trực tiếp với một database (thêm index và data migration thì đã khó khăn với 1 application). Vì vậy không tách tất cả logic của tài nguyên ra thành từng service riêng biệt mà chỉ chuyển logic **Process** sang service riêng và vẫn sử dụng monolith làm tiền đề với database (tức là không chuyển hoàn toàn từ monolith sang microservice mà chỉ chuyển nhưng phần phức tạp).

**ALB** có một tính năng khác được gọi là [path-based routing](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-listeners.html#path-conditions), định tuyến lưu lượng truy cập dựa trên đường dẫn URL đến các **target group**. Điều này có nghĩa là bạn sẽ chỉ single instance của ALB duy nhất để lưu trữ các microservice của bạn. Dịch vụ monolith sẽ nhận tất cả lưu lượng truy cập đến đường dẫn mặc định **'/'**. **Adoption và like service** sẽ lần lượt là **'/ accept' và '/ like'.**

![Microservices with AWS Fargate](/images/1-Introduce/04-arch.png?featherlight=false&width=90pc)

####  Nội dung

1. [Tạo Revision](7.1-createnewrevision/)
2. [Cập nhật Service](7.2-updateservice/)
3. [Build Docker Image](7.3-builddockerimage/)
4. [Tạo Task Definition](7.4-createtaskdefinition/)
5. [Create ECS Service](7.5-createecsservice/)