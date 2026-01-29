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

**[Screenshot: IAM Dashboard]**

The IAM dashboard displays security recommendations and current user/group status.

**[Screenshots: Creating Admin User]**

Create administrative user with console password and attach AdministratorAccess policy directly. This establishes the primary admin identity separate from root.

**[Screenshot: Admin User Login]**

Log into AWS console using the newly created admin IAM user credentials.

**[Screenshots: Creating User Groups]**

Establish user groups such as Sales and Dev teams. Attach AWS managed policies to groups for role-based access control.

**[Screenshots: Creating Standard Users]**

Provision standard IAM users and assign them to groups. Demonstrate three permission scenarios: group-based, copying from existing user, and direct policy attachment.

### S3 Bucket Configuration

**[Screenshots: S3 Bucket Creation]**

Navigate to S3 service and create a new bucket with server-side encryption using Amazon S3 managed keys (SSE-S3).

**[Screenshots: File Upload to S3]**

Upload test files to the S3 bucket to validate storage functionality and access controls.

**[Screenshots: Assigning S3 Permissions]**

Attach AmazonS3FullAccess policy to one user and AmazonS3ReadOnlyAccess to another. Verify permissions by attempting file upload with read-only user.

### EC2 Instance Deployment

**[Screenshots: EC2 Instance Launch]**

Launch EC2 instance selecting Amazon Linux 2 AMI and t2.micro instance type. Create RSA key pair for secure SSH access. Configure security group to allow access from any IP.

**[Screenshots: Custom IAM Policy Creation]**

Generate custom EC2 policy using AWS Policy Generator. Specify EC2 service, select actions like DescribeInstances and StopInstances, and input instance ARN. Copy generated JSON policy and create inline policy for user Ibrahim.

**[Screenshots: Instance Management]**

Demonstrate stopping and terminating EC2 instances under the custom IAM policy constraints.

### CloudTrail Configuration

**[Screenshots: CloudTrail Setup]**

Access CloudTrail service and review event history showing all API calls. Create a new trail to log management events. Configure trail to store logs in a dedicated S3 bucket.

### SNS Configuration

**[Screenshots: SNS Topic and Subscription]**

Create SNS topic for security alerts. Configure email subscription and confirm subscription through email verification link.

### EventBridge Integration

**[Screenshots: EventBridge Rule Creation]**

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
