[![cloud-repo-header.png](https://i.postimg.cc/fT1Xj8JG/cloud-repo-header.png)](https://postimg.cc/SJ7Jm7Ld)

# Biostasis: Cloud Infrastructure & External Services Setup Guide

Welcome to our open-source project **Biostasis**! This guide will help you set up your own cloud infrastructure using various AWS services. Also, it will help you setup the external services that we use for our application.

By following the steps outlined below, you'll be able to create an environment similar to the one used in our project.

**PS: if you do not have an experience in AWS and want to contribute to the project send an email to [emil@havetomorrow.com](mailto:emil@havetomorrow.com?subject=[GitHub]%20Source%20Han%20Sans). we will consider providing you with the credentials needed to run the application.**

## Table of content: 
  - [Before you start](#before-you-start)
  - [Introduction](#introduction)
  - [Cloud Setup Instructions](#cloud-setup-instructions)
    - [EC2](#1-ec2)
    - [RDS](#2-rds)
    - [Elasticache](#3-elasticache)
    - [Cognito](#4-cognito)
    - [SES](#5-ses)
    - [Lambda](#6-lambda)
    - [ECR](#7-ecr)
    - [ECS](#8-ecs)
    - [CloudFront](#9-cloudfront)
    - [S3](#10-s3)
    - [Elastic IP](#11-elastic-ip)
    - [Elastic Load Balancer](#12-elastic-load-balancer)
    - [Route53](#13-route53)
    - [VPC](#14-vpc)
    - [ACM Certificate](#15-acm-certificate)
  - [External Services Setup](#external-services-setup)
    - [Mailjet](#mailjet)
    - [Twilio](#twilio)
  - [Conclusion](#conclusion)

## Before you start:

Make sure you have the following:

1. An AWS account: You will need an AWS account to create and manage your cloud infrastructure.

2. AWS CLI: Install the AWS Command Line Interface (CLI) on your local machine. You can find installation instructions [Here](https://aws.amazon.com/cli/).

3. Backend Repository: Clone the backend repository of the project to access the required Docker images for ECR. You can find the repository [Here](https://github.com/tomorrowbiostasis/Biostasis-Backend).

## Introduction:

you may ask yourself: **Why you need to build your own cloud infrastructure and external services?**

we need those services to run our project and create the `.env` credentials for the [FrontEnd](https://github.com/tomorrowbiostasis/Biostasis-FrontEnd) and [BackendEnd](https://github.com/tomorrowbiostasis/Biostasis-Backend) applications to fully understand and test the whole functionality of our project. 
However, You can also surpass those steps, but then you need to modify the code and the `.env` credentials to be able to run the project properly.

## Cloud Setup Instructions

Follow the steps below to set up your cloud infrastructure:

### 1. EC2:

We will create two Linux instances: one for **SSH hosting** and another for **deep links**.

1. Launch two EC2 instances using the AWS Management Console or the AWS CLI. Make sure to select the appropriate Linux image.

2. Secure Shell (SSH) Host: Use this instance for administrative tasks and SSH access to other instances.

3. Deep Links: This instance is responsible for handling deep links functionality in our project.

### 2. RDS:

Set up an RDS instance to host the **MySQL** database.

1. Use the AWS Management Console or CLI to create an RDS instance. Choose the appropriate instance type and storage options.

2. Configure the database settings, including username, password, and database name.

### 3. Elasticache:

Create an Elasticache cluster to host the **Redis** service used in our project.

1. Use the AWS Management Console or CLI to create an Elasticache cluster.

2. Choose Redis as the caching engine and configure the necessary settings.

### 4. Cognito:

We utilize Google and Apple for authorization and authentication services through Cognito. Follow these steps to set up Cognito with the required providers:

1. Access the AWS Management Console and create a Cognito User Pool.

2. Configure the user pool settings, including identity providers such as Google and Apple.

### 5. SES:

Set up an SES domain to host the email address domain used in our project.

1. Use the AWS Management Console to create an SES domain.

2. Configure the necessary email settings and verify the domain.

### 6. Lambda:

Create an AWS Lambda function to handle the email structure for our Cognito services.

1. Use the AWS Management Console or CLI to create a Lambda function.

2. Implement the necessary logic for handling Cognito-related email workflows.

### 7. ECR:

Host the application Docker images in the Elastic Container Registry (ECR).

1. Access the AWS Management Console or use the CLI to create an ECR repository.

2. Push your Docker images to the ECR repository, which you can find in the backend repository.

### 8. ECS:

Create tasks and services in the Elastic Container Service (ECS) to deploy your Docker images from ECR.

1. Use the AWS Management Console or CLI to create an ECS cluster.

2. Define the necessary task definitions and services to deploy your Docker images.

### 9. CloudFront:

Set up a CloudFront distribution to create a public key pair.

1. Use the AWS Management Console or CLI to create a CloudFront distribution.

2. Configure the distribution settings and generate the required public and private key pair.

### 10. S3:

Create an S3 bucket to store user-uploaded files.

1. Use the AWS Management Console or CLI to create an S3 bucket.

2. Configure the bucket settings, including permissions and access control


### 11. Elastic IP:

Assign an Elastic IP to access the EC2 instance hosting the backend application.

1. Use the AWS Management Console or CLI to allocate an Elastic IP.

2. Associate the Elastic IP with the EC2 instance running the backend application.

### 12. Elastic Load Balancer:

Set up an Elastic Load Balancer to host your backend application inside the EC2 instance.

1. Use the AWS Management Console or CLI to create an Elastic Load Balancer.

2. Configure the load balancer settings and specify the backend EC2 instance as the target.

### 13. Route53:

Use Route53 to redirect traffic to your cloud infrastructure.

1. Access the AWS Management Console and create a Route53 hosted zone.

2. Configure the necessary DNS settings to redirect traffic to your cloud infrastructure.

### 14. VPC:

Set up a Virtual Private Cloud (VPC) to connect all the cloud services in one network.

1. Use the AWS Management Console or CLI to create a VPC.

2. Configure the necessary subnets, route tables, and security groups.

### 15. ACM Certificate:

Obtain an ACM certificate to certify the domain name used to host the backend.

1. Use the AWS Management Console or CLI to request an ACM certificate.

2. Configure the certificate settings and verify domain ownership.

## External Services Setup:

In addition to the cloud infrastructure, our open-source project requires the integration of external services to enable certain functionalities. This section will guide you through the process of setting up the following external services: Mailjet for email templates and Twilio for sending SMS messages to users.

### Mailjet

Mailjet is used to create transactional email templates for specific purposes within our project. Follow the steps below to set up Mailjet and configure the required email templates:

1. Sign up for a Mailjet account at [https://www.mailjet.com/](https://www.mailjet.com/) if you don't have one already.

2. Once logged in to your Mailjet account, navigate to the "Transactional Email" section.

3. Create a new transactional email template for each of the following purposes:

   a. **User Change Email**: This template should be used when a user changes their email address.

   b. **Emergency Message without Location**: This template should be used to send an email when a user reports an emergency situation without providing location data.

   c. **Emergency Message with Location**: This template should be used to send an email when a user reports an emergency situation with location data.

   d. **Data Export**: This template should be used to send an email containing exported user data for compliance with GDPR regulations.

4. Customize each template according to the project's requirements. You can use the Mailjet template editor to design the email content and incorporate dynamic variables as needed.

5. Make note of the template IDs or any other necessary credentials provided by Mailjet, as you will need them for the integration with the project.

### Twilio

Twilio is used to send SMS messages to users. To set up Twilio for our project, follow these steps:

1. Sign up for a Twilio account at [https://www.twilio.com/](https://www.twilio.com/) if you don't have one already.

2. Once you have logged in to your Twilio account, navigate to the console.

3. Obtain your Account SID and Auth Token from the Twilio dashboard. These will be used for authentication when making API requests.

4. To send SMS messages, you will need to have a Twilio phone number. You can either purchase a new number or use an existing one.

5. Make sure you have the Twilio SDK or client library installed in your project, depending on your programming language of choice. Refer to the Twilio documentation for detailed instructions on integrating Twilio into your project.

6. Implement the necessary logic in your project to utilize the Twilio API and send SMS messages to users.

That's it! You have now successfully set up the external services required for our open-source project. Make sure to configure the necessary credentials and endpoints within your project code to enable the integration with Mailjet for email templates and Twilio for sending SMS messages to users.

## Conclusion:

Congratulations! You have successfully set up your own cloud infrastructure using various **AWS** services. In addition, you setup **Mailjet** and **Twilio** to be able to send emails and sms messages. 

You can now start using the infrastructure for the project and make any necessary customizations. If you encounter any issues or have any questions, refer to the documentation or add your question on the discussion page of this repository.

Thank you for contributing to the **Biostasis** project!
