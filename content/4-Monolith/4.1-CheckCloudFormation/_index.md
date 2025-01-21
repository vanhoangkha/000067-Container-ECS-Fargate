---
title : "Testing CloudFormation"
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---

#### Check CloudFormation

1. Access to **CloudFormation**

- Select the created **stack**
- Choose the **Resources** tab
- Search for the s3 bucket with the Logical ID **"MythicalBucket"**
- Click on the Physical ID of the bucket to open the S3 console

![Check CloudFormation](/images/4-Monolith/4.1-CheckCloudFormation/a0001-cfn.png?featherlight=false&width=90pc)

- On the Bucket Console, choose **Permissions**

![Check CloudFormation](/images/4-Monolith/4.1-CheckCloudFormation/a0002-s3.png?featherlight=false&width=90pc)

Add the following code to your bucket policy:
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

2. Return to **CloudFormation**

- Select the created **stack**
- Select **Outputs**
- Select **S3WebsiteURL**

![Check CloudFormation](/images/4-Monolith/4.1-CheckCloudFormation/0001-checkcloudformation.png?featherlight=false&width=90pc)

3. Use your browser to access **S3WebsiteURL**.

![Check CloudFormation](/images/4-Monolith/4.1-CheckCloudFormation/0002-checkcloudformation.png?featherlight=false&width=90pc)

#### About the website Mythical Mysfits

Mythical Mysfits is a (fictional) pet adoption nonprofit dedicated to helping abandoned and often misunderstood mythical creatures find a forever new family! Mythical Mysfits believe that all creatures deserve a second chance, even if they take their first chance to hide under bridges and rob them of gratuitous acts of helplessness.

Our business has thrived with a single Mysfits adoption center, located inside Devil Tower National Monument. Talk, friends, and join if you visit.

We've just had a bunch of new mystics arriving at our doorstep with nowhere else to go! They're all pretty distraught after not only being evicted from their home... but a grumpy goblin who also denied them all entry to a swamp they used to hide. hide in the past.

That's why we hired you to be our **Full Stack Engineer**. We needed a more scalable way to showcase our treasure trove of mysteries and let families adopt them. We want you to build your first Mythical Mysfits adoption website to help introduce these adorable, wondrous, often mischievous creatures to the world!
