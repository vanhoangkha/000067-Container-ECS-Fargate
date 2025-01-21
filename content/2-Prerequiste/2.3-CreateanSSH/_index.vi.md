---
title : "Tạo SSH Key"
weight : 3 
chapter : false
pre : " <b> 2.3 </b> "
---

#### Tạo SSH key


1. Chúng ta thực hiện lệnh để **generate SSH key** trong Cloud9. Key này sẽ được sử dụng truy cập vào node  instance

{{% notice info %}}
Chúng ta có thể truy cập bằng lệnh: **```ssh -i PRIVATE_KEY.PEM ec2-user @ EC2_PUBLIC_DNS_NAME```**
{{% /notice %}}

```
ssh-keygen
```

![Set up](/images/2-Prerequiste/2.3-CreateanSSH/0001-createssh.png?featherlight=false&width=90pc)

2. Chúng ta thực hiện **upload** public key vào **EC2 region**

```bash
aws ec2 import-key-pair --key-name "mythicaleks" --public-key-material file://~/.ssh/id_rsa.pub
```

{{% notice tip %}}
Nếu gặp lỗi **An error occurred (InvalidKey.Format) when calling the ImportKeyPair operation: Key is not in valid OpenSSH public key format**, bạn có thể thử lệnh sau:
{{% /notice %}}

```bash
aws ec2 import-key-pair --key-name "mythicaleks" --public-key-material fileb://~/.ssh/id_rsa.pub
```

![Set up](/images/2-Prerequiste/2.3-CreateanSSH/0002-createssh.png?featherlight=false&width=90pc)

3. Truy cập vào **[EC2](https://ap-southeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-southeast-1#KeyPairs:)**

- Chọn **Key pair**
- Xem key đã được tải lên region hiện tại

![Set up](/images/2-Prerequiste/2.3-CreateanSSH/0003-createssh.png?featherlight=false&width=90pc)


