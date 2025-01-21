---
title : "Generate SSH Key"
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---

#### Generate SSH key


1. We execute the command to **generate SSH key** in Cloud9. This key will be used to access the node instance

{{% notice info %}}
We can access it with the command: **```ssh -i PRIVATE_KEY.PEM ec2-user@EC2_PUBLIC_DNS_NAME```**
{{% /notice %}}

```bash
ssh-keygen
```

![Set up](/images/2-Prerequiste/2.3-CreateanSSH/0001-createssh.png?featherlight=false&width=90pc)

2. We do **upload** public key to **EC2 region**

```bash
aws ec2 import-key-pair --key-name "lab67mythical" --public-key-material file://~/.ssh/id_rsa.pub
```

{{% notice tip %}}
If you get the error **An error occurred (InvalidKey.Format) when calling the ImportKeyPair operation: Key is not in valid OpenSSH public key format**, you can try the following command:
{{% /notice %}}

```bash
aws ec2 import-key-pair --key-name "lab67mythical" --public-key-material fileb://~/.ssh/id_rsa.pub
```

![Set up](/images/2-Prerequiste/2.3-CreateanSSH/0002-createssh.png?featherlight=false&width=90pc)

3. Go to **[EC2](https://ap-southeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-southeast-1#KeyPairs:)**

- Select **Key pair**
- See the you've **uploaded** to the current region

![Set up](/images/2-Prerequiste/2.3-CreateanSSH/0003-createssh.png?featherlight=false&width=90pc)