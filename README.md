# AWS Cloud Baseline Security Implementation

## Project Overview

This project demonstrates the practical implementation of AWS baseline security controls across core services. The lab environment establishes identity and access management structures, secure storage configurations, compute instance controls, and automated monitoring using CloudTrail, EventBridge, and SNS. This work validates hands-on competency in building secure cloud infrastructure from the ground up.

## Objectives

- Configure administrative and non-administrative IAM users with least privilege access
- Create user groups and apply role-based permissions using AWS managed and custom policies
- Deploy and secure S3 buckets with server-side encryption and access controls
- Launch and manage EC2 instances with custom IAM policies and secure key pair authentication
- Enable CloudTrail logging and create trails for comprehensive audit tracking
- Configure SNS topics and email subscriptions for automated security notifications
- Implement EventBridge rules to monitor specific API calls and trigger real-time alerts

## Lab Architecture

The environment operates within a single AWS account with a root user managing initial IAM configuration. An administrative IAM user is created with full AdministratorAccess privileges to handle subsequent configurations. Multiple standard users are provisioned and organized into groups with targeted permissions. S3 buckets store uploaded files with server-side encryption enabled. EC2 instances are launched with RSA key pair authentication and security group rules permitting SSH access. CloudTrail captures all API activity across services and stores logs in a dedicated S3 bucket. EventBridge monitors CloudTrail events for specific actions such as S3 bucket creation. SNS topics send email notifications when monitored events are detected. Access control is enforced through a combination of inline policies, AWS managed policies, and custom JSON policies generated via the AWS Policy Generator.

## Tools and Technologies

- AWS IAM (Identity and Access Management)
- AWS S3 (Simple Storage Service) with SSE-S3 encryption
- AWS EC2 (Elastic Compute Cloud)
- AWS CloudTrail for API logging and audit trails
- Amazon EventBridge for event-driven automation
- Amazon SNS (Simple Notification Service)
- AWS Policy Generator for custom policy creation
- Amazon Linux 2 AMI for EC2 instances

## Step-by-Step Implementation Summary with Screenshots

### IAM Configuration

**<img src="https://imgur.com/N0Fwy9Q.png" />**

Access AWS root account and navigate to IAM service through the console search bar.

**<img width="975" height="469" alt="image" src="https://github.com/user-attachments/assets/63b9eb15-4766-4d29-86bf-225350ccc128" />**

The IAM dashboard displays security recommendations and current user/group status.

**<img width="975" height="464" alt="image" src="https://github.com/user-attachments/assets/c149ecd7-f7ef-470d-aef5-ebf3192c929c" />**
**<img width="975" height="466" alt="image" src="https://github.com/user-attachments/assets/dd316faa-a2a7-40ef-af61-1654bcd69ed3" />**

Create administrative user with console password and attach AdministratorAccess policy directly. This establishes the primary admin identity separate from root.

**<img width="975" height="466" alt="image" src="https://github.com/user-attachments/assets/3ebf9e77-4436-4bc2-8568-66553b4c3f1c" />**
**<img width="975" height="467" alt="image" src="https://github.com/user-attachments/assets/b23986e1-1052-445d-a918-ec4434206257" />**
**<img width="975" height="465" alt="image" src="https://github.com/user-attachments/assets/eb858349-5eeb-4981-be8f-5d6a3dc61274" />**

Log into AWS console using the newly created admin IAM user credentials.

**<img width="975" height="467" alt="image" src="https://github.com/user-attachments/assets/5479b38f-ac9e-4758-954b-147bffb5c428" />**
**<img width="975" height="461" alt="image" src="https://github.com/user-attachments/assets/254271d9-856f-44db-a4eb-b68eaf044870" />**
**<img width="975" height="465" alt="image" src="https://github.com/user-attachments/assets/dae49479-4f37-4354-9a89-d6a1867d5295" />**
**<img width="975" height="459" alt="image" src="https://github.com/user-attachments/assets/bde15c30-7fea-440d-8231-6be7c1f03cb0" />**

Establish user groups such as Sales and Dev teams. Attach AWS managed policies to groups for role-based access control.

**<img width="975" height="462" alt="image" src="https://github.com/user-attachments/assets/988268ed-c0da-4137-8797-8ab9c82fe8dd" />**
**<img width="975" height="462" alt="image" src="https://github.com/user-attachments/assets/06b6770e-6114-4149-85b5-6a8f14d4c1ef" />**
**<img width="975" height="435" alt="image" src="https://github.com/user-attachments/assets/8de1e1ff-bcbe-4b0b-90be-bd6b340692c9" />**

Provision standard IAM users and assign them to groups. Demonstrate three permission scenarios: group-based, copying from existing user, and direct policy attachment.

### S3 Bucket Configuration

**<img width="975" height="307" alt="image" src="https://github.com/user-attachments/assets/f77bf0c0-3590-453e-97fd-114c97c8fc81" />**

Navigate to S3 service and create a new bucket with server-side encryption using Amazon S3 managed keys (SSE-S3).

**<img width="975" height="462" alt="image" src="https://github.com/user-attachments/assets/06eaeca6-234c-44c8-b0ea-978ef4f09dfd" />**
**<img width="975" height="464" alt="image" src="https://github.com/user-attachments/assets/386f66d4-4e00-4761-b044-333a78b0c83b" />**
**<img width="975" height="465" alt="image" src="https://github.com/user-attachments/assets/48df8cdd-818c-4e20-8fe3-4a61691ceb58" />**

Upload test files to the S3 bucket to validate storage functionality and access controls.

**<img width="975" height="462" alt="image" src="https://github.com/user-attachments/assets/ba1d2acc-66f5-41bb-9793-c983a3a33142" />**
**<img width="975" height="463" alt="image" src="https://github.com/user-attachments/assets/d8356885-354b-49e6-8e32-2231da23bd48" />**
**<img width="975" height="460" alt="image" src="https://github.com/user-attachments/assets/bcc77fbb-ab27-4adc-ba4c-7475c74cb070" />**

Attach AmazonS3FullAccess policy to one user and AmazonS3ReadOnlyAccess to another. Verify permissions by attempting file upload with read-only user.

### EC2 Instance Deployment

**<img width="975" height="460" alt="image" src="https://github.com/user-attachments/assets/a16cb44d-6034-4a36-8c7c-b82fe6e4451d" />**
**<img width="975" height="466" alt="image" src="https://github.com/user-attachments/assets/a7d534ad-13af-4373-8b42-0dd50414717c" />**
**<img width="975" height="460" alt="image" src="https://github.com/user-attachments/assets/fc153150-6430-46dd-91ba-853b2cb6fede" />**
**<img width="975" height="463" alt="image" src="https://github.com/user-attachments/assets/7eddc4eb-720d-4e27-a510-85722565cbb7" />**
**<img width="975" height="462" alt="image" src="https://github.com/user-attachments/assets/805233e4-a3a5-430c-80ae-a91b1395aef4" />**

Launch EC2 instance selecting Amazon Linux 2 AMI and t2.micro instance type. Create RSA key pair for secure SSH access. Configure security group to allow access from any IP.

**<img width="975" height="463" alt="image" src="https://github.com/user-attachments/assets/678fb5de-5aab-4a1e-90e0-250bfddcb021" />**
**<img width="975" height="461" alt="image" src="https://github.com/user-attachments/assets/232c0393-453d-4499-8dfa-82b18065bad9" />**

Generate custom EC2 policy using AWS Policy Generator. Specify EC2 service, select actions like DescribeInstances and StopInstances, and input instance ARN. Copy generated JSON policy and create inline policy for user Ibrahim.

**<img width="975" height="465" alt="image" src="https://github.com/user-attachments/assets/366d410d-5a24-401b-aa94-d4e6c8244b88" />**
**<img width="975" height="468" alt="image" src="https://github.com/user-attachments/assets/86d74022-9753-42ea-97a1-fe9ebbf4feab" />**
**<img width="975" height="448" alt="image" src="https://github.com/user-attachments/assets/b17fc362-840e-481f-8fd5-f5e16ef64c06" />**

Demonstrate stopping and terminating EC2 instances under the custom IAM policy constraints.

### CloudTrail Configuration

**<img width="975" height="467" alt="image" src="https://github.com/user-attachments/assets/1bd03ae1-5cc2-4ee3-b4b3-931a6f59303f" />**
**<img width="975" height="464" alt="image" src="https://github.com/user-attachments/assets/6e349340-21e6-4b07-bf4c-91b8a06a2b15" />**
**<img width="975" height="464" alt="image" src="https://github.com/user-attachments/assets/2146f3e1-588c-472d-bb1a-10d351261a86" />**
**<img width="975" height="463" alt="image" src="https://github.com/user-attachments/assets/1568c124-a46e-415c-953c-5f3434361f0d" />**

Access CloudTrail service and review event history showing all API calls. Create a new trail to log management events. Configure trail to store logs in a dedicated S3 bucket.

### SNS Configuration

**<img width="975" height="462" alt="image" src="https://github.com/user-attachments/assets/04fd75cd-b057-495d-98b1-8ded203a0d9a" />**
**<img width="975" height="461" alt="image" src="https://github.com/user-attachments/assets/26928fc9-e091-439a-9a28-43beda67ff1e" />**
**<img width="975" height="460" alt="image" src="https://github.com/user-attachments/assets/8cec586e-1c82-4f1c-a18b-c1e6d682433e" />**

Create SNS topic for security alerts. Configure email subscription and confirm subscription through email verification link.

### EventBridge Integration

**<img width="975" height="463" alt="image" src="https://github.com/user-attachments/assets/d45a8e9e-95a7-4b0f-9978-299ae0a2c09f" />**
**<img width="975" height="462" alt="image" src="https://github.com/user-attachments/assets/db2ef5e7-1563-487e-8cbb-3fa953c10e17" />**
**<img width="975" height="464" alt="image" src="https://github.com/user-attachments/assets/ecf675b9-8927-4d4e-aee0-4d63cd59ae1d" />**
**<img width="975" height="465" alt="image" src="https://github.com/user-attachments/assets/f2cd940e-f073-4793-8f75-800bc6b72f5c" />**
**<img width="975" height="467" alt="image" src="https://github.com/user-attachments/assets/848676a4-36be-4e0a-adc9-a1f6ad6835e9" />**

Create EventBridge rule to monitor CloudTrail API calls. Configure event pattern to trigger on CreateBucket events. Edit JSON pattern to specify exact event name. Set SNS topic as target for notifications. Validate by creating a new S3 bucket and receiving email alert.

## Security Concepts Demonstrated

This project implements multiple security principles critical to cloud infrastructure protection. Identity and access management is enforced through separation of root and administrative accounts, least privilege access via user groups, and granular permissions using both AWS managed and custom policies. Data protection is achieved through S3 server-side encryption and access control lists. Authentication security is strengthened by RSA key pair encryption for EC2 instance access. Comprehensive audit logging captures all API activity via CloudTrail with centralized log storage. Event-driven security monitoring detects specific actions in real-time and triggers automated notifications. Role-based access control organizes users into functional groups with targeted permissions. Policy validation confirms permissions work as intended through practical testing scenarios.

## Key Learning Outcomes

This project demonstrates the ability to implement foundational AWS security controls across multiple service layers. The work shows practical competency in identity management, secure resource provisioning, policy creation and enforcement, audit logging configuration, and automated security monitoring. The implementation reflects understanding of AWS security best practices including least privilege access, encryption at rest, comprehensive logging, and event-driven incident response. This lab validates hands-on experience building secure cloud infrastructure suitable for production environments.

## How to Reproduce the Lab

1. Create an AWS account and access the root console
2. Navigate to IAM and create an administrative user with AdministratorAccess policy
3. Log in as the admin user and create user groups with appropriate managed policies
4. Provision standard users and assign them to groups or attach policies directly
5. Create S3 bucket with SSE-S3 encryption and upload test files
6. Launch EC2 instance with Amazon Linux 2 AMI and create RSA key pair
7. Use AWS Policy Generator to create custom EC2 policies with specific actions
8. Enable CloudTrail and create a trail logging to S3
9. Configure SNS topic with email subscription
10. Create EventBridge rule monitoring CloudTrail events and targeting SNS topic
11. Test all configurations by performing actions and verifying expected behavior

## Project Status

This project is complete and fully functional. The implementation can be expanded to include additional services such as AWS GuardDuty for threat detection, AWS Config for compliance monitoring, VPC flow logs for network analysis, and multi-region configurations for high availability scenarios.
