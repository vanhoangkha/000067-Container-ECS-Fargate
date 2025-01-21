---
title : "Microservices with AWS Fargate"
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

#### Microservices with AWS Fargate

In this lab, we will break the monolith into microservices.

Monolith provides different API resources on other routes to fetch information about **Mysfits**, **like** or **adopt** experiences

The logic of these resources includes some **proccess** (like making sure that the user is authorized to perform a specific action, that Mysfit is eligible to apply, etc.) with **persistence layer** (specifically DynamoDB).

Instead of using many different services that interact directly with a database (adding indexes and data migrations is difficult with an application). So do not separate all the logic of the resource into a separate service, but only move the **Process** logic to a separate service and still use monolith as a premise with the database (ie, do not completely switch from monolith to microservice but only transfer but the complex part).

**ALB** has another feature called [path-based routing](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-listeners.html#path-conditions) , which routes traffic based on URL paths to **target groups**. This means you will only have single instance of ALB to host your microservices. The monolith service will receive all traffic to the default path **'/'**. **Adoption and like service** will be **'/accept' and '/like' respectively.**

![Microservices with AWS Fargate](/images/1-Introduce/04-arch.png?featherlight=false&width=90pc)

####  Content

1. [Create Revision](7.1-createnewrevision/)
2. [Update Service](7.2-updateservice/)
3. [Build Docker Image](7.3-builddockerimage/)
4. [Create Task Definition](7.4-createtaskdefinition/)
5. [Create ECS Service](7.5-createecsservice/)