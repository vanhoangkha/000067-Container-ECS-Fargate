---
title : "Create Revision"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 7.1 </b> "
---

#### Create Revision

1. In the First step, we add some glue code in **monolith** to turn the **like** function into a separate service (microservice). In the lab, use **Cloud9** and find the **app/monolith-service/service/mythicalMysfitsService.py** file. Then do uncomment the following code:

```
# @app.route("/mysfits/<mysfit_id>/fulfill-like", methods=['POST'])
# def fulfillLikeMysfit(mysfit_id):
# serviceResponse = mysfitsTableClient.likeMysfit(mysfit_id)
# flaskResponse = Response(serviceResponse)
# flaskResponse.headers["Content-Type"] = "application/json"
# return flaskResponse
```

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0001-createrevision.png?featherlight=false&width=90pc)

2. With the new feature added **monolith**, we rebuild the monolith docker image with a new tag (nolike).

```
 cd ~/environment/amazon-ecs-mythicalmysfits-workshop/workshop-1/app/monolith-service
 MONO_ECR_REPOSITORY_URI=$(aws ecr describe-repositories | jq -r .repositories[].repositoryUri | grep mono)
 docker build -t monolith-service:nolike .
```
![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0002-createrevision.png?featherlight=false&width=90pc)

3. Execute **push** monolith docker image onto **ECR**

- It is best to avoid the latest tag, which can be ambiguous. Instead, choose a unique tag, descriptive name, or preferably a Git SHA and/or version ID).

```
 docker tag monolith-service:nolike $MONO_ECR_REPOSITORY_URI:nolike
 docker push $MONO_ECR_REPOSITORY_URI:nolike
```

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0003-createrevision.png?featherlight=false&width=90pc)

4. Check whether the monolith docker image has been pushed to the ECR?

- Access to **ECS**
- Select **Task Definitions**
- Select **Monolith-Definitions-STACK_NAME** (save you may be different in the picture because the following part depends on the STACK_NAME you set)

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0004-createrevision.png?featherlight=false&width=90pc)

5. Then select **Monolith-Definition-STACK_NAME** revision 2.

- Select **Create new revision**

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0005-createrevision.png?featherlight=false&width=90pc)

6. Go to **ECR** to view the repositories. Now, in the **Images** section, there are 2 images with 2 tags: latest and **nolike**.

- Copy **Image URI**

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0006-createrevision.png?featherlight=false&width=90pc)

7. Use **Image URI** tag **nolike** to create **New revision**

- Configure **Container**
- Replace **Image URI** with **Image URI** tag **nolike**

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0007-createrevision.png?featherlight=false&width=90pc)

8. Select **Create**

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0008-createrevision.png?featherlight=false&width=90pc)

9. Finish creating **Monolith-Definition-STACK_NAME** revision 3.

![ Microservices with AWS Fargate](/images/7-microservices/7.1-Createnewrevision/0009-createrevision.png?featherlight=false&width=90pc)