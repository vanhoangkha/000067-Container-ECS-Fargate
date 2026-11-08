# Monolithic app to Microservices with Docker, ECS and AWS Fargate

> Running containers on Amazon ECS with Fargate.

A hands-on workshop from the [AWS First Cloud Journey](https://github.com/vanhoangkha/aws-first-cloud-journey) series, available in English and Vietnamese.

**Read the workshop online:** https://vanhoangkha.github.io/000067-Container-ECS-Fargate/

## Overview

Docker is a software platform that allows you to quickly build, test, and deploy applications. Docker packages software into standardized units called containers that have everything the software needs to run, including libraries, system tools, code, and runtimes. Using Docker, you can quickly deploy and scale your application into any environment and know with certainty that your code will run. Running Docker on AWS gives developers and administrators a low-cost and highly reliable way to build, ship, and run distributed applications of any size.

Docker works by providing a standard method for running your code. Docker is an operating system for containers. In the same way that a virtual machine virtualizes (eliminating the need to directly manage) server hardware, containers virtualize the host's operating system. Docker is installed on each host and provides simple commands that you can use to build, start, or stop containers.

## Workshop contents

1. Introduction
2. Preparation
   - Create your CloudFormation Stack
   - Setup your environment
   - Generate SSH Key
3. Introducing Docker and Containers
   - Docker Basics
   - Container image
4. Containerize monolith
   - Testing CloudFormation
   - Containerize the Mythical Mysfits monolith
5. Deploy the container using AWS Fargate
6. ALB and ECS Service
7. Microservices with AWS Fargate
   - Create Revision
   - Update Service
   - Build Docker Image
   - Create Task Definition
   - Create ECS Service
8. Clean up resources

## Prerequisites

- An AWS account with permissions to create the resources used in the labs
- Basic familiarity with the AWS Management Console
- [Hugo](https://gohugo.io/installation/) (extended edition) if you want to run the site locally

## Run locally

```bash
git clone https://github.com/vanhoangkha/000067-Container-ECS-Fargate.git
cd 000067-Container-ECS-Fargate
hugo server
```

Then open http://localhost:1313 in your browser.

## Repository structure

| Path | Purpose |
| --- | --- |
| `content/` | Workshop pages (`*.md` English, `*.vi.md` Vietnamese) |
| `static/` | Images and other static assets |
| `layouts/` | Hugo layout overrides |
| `themes/` | Hugo theme |
| `config.toml` | Site configuration |

## Cost and cleanup

The labs create AWS resources that may incur charges. Complete the **Clean up** chapter when you finish to remove them.

## Contributing

Contributions are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

To report a security issue, see [SECURITY.md](SECURITY.md).

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE).
