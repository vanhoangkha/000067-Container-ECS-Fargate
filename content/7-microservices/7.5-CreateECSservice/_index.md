---
title : "Create ECS Service"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 7.5 </b> "
---

1. Also in the newly created Task interface, we will create an ECS service to run the newly created Task definition.

- Select **Deploy**
- Select **Create Service**

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0001-createecsservice.png?featherlight=false&width=90pc)

2. Setting up the environment

- Select cluster (**Cluster-STACK_NAME**)

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0002-createecsservice.png?featherlight=false&width=90pc)

3. Perform configuration ***Deployment**

- **Application type**, default **Service**
- Perform naming **Service name**
- **Desired tasks**, choose 1

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0003-createecsservice.png?featherlight=false&width=90pc)

4. Configure **Load Balancing**

- Select **Application Load Balancer**
- Select **Use an existing load balancer**
- Select **alb-STACK_NAME**
- Configure **Listener** (**Port**: 80 and **Protocol**: HTTP)
- Create **Target group**, enter **```microservice-tg```**
- **Health check path**, enter **/**
- **Health check grace period**, enter **300**

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0004-createecsservice.png?featherlight=false&width=90pc)

5. Configure **Network**

- **VPC**, select **Mysfits-STACK_NAME**
- **Subnets**, choose private subnet
- Go to **Security group**, select **Use an existing security group**
- We choose **Security group** default and make sure to configure inbound **HTTP** (port 80)
- Select **Deploy**

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0005-createecsservice.png?featherlight=false&width=90pc)

6. Thus, we create the service deploy successfully.

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0006-createecsservice.png?featherlight=false&width=90pc)

7. After the Microservice service deploys, we test the website interface and perform the like test.

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0007-createecsservice.png?featherlight=false&width=90pc)

8. We use the browser to access the website. Check **CloudWatch logs** again and show **"Like processed."**

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0008-createecsservice.png?featherlight=false&width=90pc)

9. Implement endpoint removal from monolith using Cloud9.

- In the monolith folder, open **mythicalMysfitsService.py** find the following code:

```
# increment the number of likes for the provided mysfit.
@app.route("/mysfits/<mysfit_id>/like", methods=['POST'])
def likeMysfit(mysfit_id):
    serviceResponse = mysfitsTableClient.likeMysfit(mysfit_id)
    process_like_request()
    flaskResponse = Response(serviceResponse)
    flaskResponse.headers["Content-Type"] = "application/json"
    return flaskResponse
```

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/0009-createecsservice.png?featherlight=false&width=90pc)

10. Then we build a monolith image

```
 cd ~/environment/amazon-ecs-mythicalmysfits-workshop/workshop-1/app/monolith-service
 docker build -t monolith-service:nolike2 .
```

![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/00010-createecsservice.png?featherlight=false&width=90pc)

11. Perform tag assignment and push to monolith ECR repository.

- We use the tag: nolike2.

```
 docker tag monolith-service:nolike2 $MONO_ECR_REPOSITORY_URI:nolike2
 docker push $MONO_ECR_REPOSITORY_URI:nolike2
```
<!-- ![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/00011-createecsservice.png?featherlight=false&width=90pc) -->

12. Check **monolith repository** on ECR, we will see that the image is pushed with the tag nolike2.
<!-- 
![ Microservices with AWS Fargate](/images/7-microservices/7.5-CreateECSservice/00012-createecsservice.png?featherlight=false&width=90pc) -->

13. Now make one last Task Definition for the monolith to refer to this new container image URI (this process should be familiar now, and you can probably see that it makes sense to leave this drudgery to a CI/CD service in production), update the monolith service to use the new Task Definition, and make sure the app still functions as before