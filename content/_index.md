---
title : "Monolithic app to Microservices with Docker, ECS and AWS Fargate"
weight : 1 
chapter : false
---

# Monolithic app to Microservices with Docker, ECS and AWS Fargate

#### Overview

Docker is a software platform that allows you to quickly build, test, and deploy applications. Docker packages software into standardized units called containers that have everything the software needs to run, including libraries, system tools, code, and runtimes. Using Docker, you can quickly deploy and scale your application into any environment and know with certainty that your code will run.
Running Docker on AWS gives developers and administrators a low-cost and highly reliable way to build, ship, and run distributed applications of any size.

{{% notice info %}}
Docker partners with AWS to help developers quickly bring modern applications to the cloud. This partnership helps developers using Docker Compose and Docker Desktop to leverage the same local workflows they use today to seamlessly deploy applications on Amazon ECS and AWS Fargate.
{{% /notice %}}

#### How Docker works

Docker works by providing a standard method for running your code. Docker is an operating system for containers. In the same way that a virtual machine virtualizes (eliminating the need to directly manage) server hardware, containers virtualize the host's operating system. Docker is installed on each host and provides simple commands that you can use to build, start, or stop containers.

AWS services like **AWS Fargate, Amazon ECS, Amazon EKS, and AWS Batch** make it easy to run Docker containers at scale.

![Docker basic](/images/1-Introduce/0001-docker.png?featherlight=false&width=60pc)

In the lab, we will be converting a **Monolithic app** to **Microservices** with **Docker**, **ECS** and **AWS Fargate**