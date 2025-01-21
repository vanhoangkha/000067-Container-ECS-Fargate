---
title : "Kiểm tra CloudFormation"
weight : 1 
chapter : false
pre : " <b> 4.1 </b> "
---

#### Kiểm tra CloudFormation

1. Truy cập vào **CloudFormation**

- Chọn **stack** đã tạo
- Chọn thẻ **Resources**
- Tìm S3 Bucket có Logical ID là **"MythicalBucket"**
- Nhấn vào Physical ID của Bucket để truy cập bảng điều khiển của bucket

![Check CloudFormation](/images/4-Monolith/4.1-CheckCloudFormation/a0001-cfn.png?featherlight=false&width=90pc)

- Tại bảng điều khiển bucket, chọn thẻ **Permissions**

![Check CloudFormation](/images/4-Monolith/4.1-CheckCloudFormation/a0002-s3.png?featherlight=false&width=90pc)

Thêm đoạn mã sau vào Bucket Policy:

```json
{
    "Version": "2012-10-17",
    "Id": "PutObjPolicy",
    "Statement": [
        {
            "Sid": "DenyObjectsThatAreNotSSEKMS",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<replace-with-your-bucket-name>/*"
        }
    ]
}
```
![Check CloudFormation](/images/4-Monolith/4.1-CheckCloudFormation/a0003-s3.png?featherlight=false&width=90pc)

2. Quay về giao diện **CloudFormation**

- Mở stack đã tạo
- Mở thẻ **Output**
- Tìm khóa **S3WebsiteURL**

![Check CloudFormation](/images/4-Monolith/4.1-CheckCloudFormation/0001-checkcloudformation.png?featherlight=false&width=90pc)

3. Sử dụng trình duyệt truy cập qua giá trị trả về của **S3WebsiteURL**.

![Check CloudFormation](/images/4-Monolith/4.1-CheckCloudFormation/0002-checkcloudformation.png?featherlight=false&width=90pc)

#### Giới thiệu về website Mythical Mysfits

Mythical Mysfits là một tổ chức phi lợi nhuận nhận nuôi thú cưng (hư cấu) chuyên giúp đỡ những sinh vật thần thoại bị bỏ rơi và thường bị hiểu lầm tìm thấy một gia đình mãi mãi mới! Mythical Mysfits tin rằng tất cả các sinh vật đều xứng đáng có cơ hội thứ hai, ngay cả khi chúng dành cơ hội đầu tiên để trốn dưới gầm cầu và cướp đi những hành động bất lực một cách vô cớ.

Công việc kinh doanh của chúng tôi đã phát triển mạnh chỉ với một trung tâm nhận con nuôi Mysfits duy nhất, nằm bên trong Đài tưởng niệm Quốc gia Devil Tower. Nói chuyện, bạn bè và tham gia nếu bạn đến thăm.

Chúng tôi vừa có một loạt những điều thần bí mới đến trước cửa nhà chúng tôi mà không còn nơi nào khác để đi! Tất cả họ đều khá quẫn trí sau khi không chỉ bị đuổi khỏi nhà của họ ... mà một con yêu tinh vô cùng gắt gỏng cũng đã từ chối tất cả sự nhập cảnh của họ tại một đầm lầy mà họ từng làm nơi ẩn náu trong quá khứ.

Đó là lý do tại sao chúng tôi đã thuê bạn làm **Full Stack Engineer** của chúng tôi. Chúng tôi cần một cách có thể mở rộng hơn để giới thiệu kho bí ẩn của chúng tôi và để các gia đình áp dụng chúng. Chúng tôi muốn bạn xây dựng trang web tiếp nhận Mythical Mysfits đầu tiên để giúp giới thiệu những sinh vật đáng yêu, kỳ diệu, thường tinh nghịch này với thế giới!