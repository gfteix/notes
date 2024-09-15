---
created-date: 2023-09-03
---

Notes taken while studying for the AWS Cloud Practitioner Certification. It is really disorganized.


# AWS Cloud Practitioner Certification Study Notes

### Amazon Macie

- **Purpose**: Detects sensitive data.

### Amazon Shield

- **Purpose**: Protects against DDoS attacks.

### AWS Core Concepts

- **Key Principle**: Pay for what you use.
- **Cloud Computing**: On-demand delivery of resources over the internet with pay-as-you-go pricing.

---

## Amazon EC2 (Elastic Compute Cloud)

- EC2 enables **multitenancy**: sharing underlying hardware between virtual machines.
- With EC2, you can:
    - Choose the operating system.
    - Select the number of instances.
    - Control what runs in your instance (e.g., business apps, web apps, databases, third-party software).
- **Vertical Scaling**: Add more CPU and memory.
- **Advantage**: While virtual machines aren't new, EC2 simplifies provisioning, allowing for quick scaling.

### EC2 Instance Families

- **General Purpose**: Balanced resources for diverse workloads like web services.
- **Compute Optimized**: Ideal for gaming and high-performance computing.
- **Memory Optimized**: For memory-intensive applications.
- **Accelerated Computing**: Designed for floating-point number calculations, graphics processing, etc.
- **Storage Optimized**: Designed for high performance, delivering tens of thousands of low-latency IOPS.

### EC2 Pricing Models

- **On-Demand**: Pay for the duration your instance runs.
- **Saving Plan**: Lower prices in exchange for a commitment (1–3 year terms).
- **Reserved Instances**: Suitable for predictable workloads.
- **Spot Instances**: AWS can reclaim the instance when needed.
- **Dedicated Hosts**: Physical servers dedicated to your use.

---

## EC2 Auto Scaling and Elastic Load Balancing

- **Scalability**: Start with what you need and scale automatically as demand changes.
- **Elastic Load Balancing (ELB)**: Distributes incoming traffic across multiple EC2 instances.
- ELB acts as a single point of contact and spreads requests across resources in the Auto Scaling group.

---

## Serverless Computing

- **Definition**: Your code runs on servers managed by AWS, without provisioning or managing them.
- **Benefits**: Focus on innovation, and applications can scale automatically.

### AWS Serverless Services

- **Amazon ECS (Elastic Container Service)**: Container management system to run and scale containerized applications.
- **Amazon EKS (Elastic Kubernetes Service)**: Fully managed Kubernetes on AWS.
- **AWS Fargate**: Serverless compute engine for containers, managing the server infrastructure for you.

---

## Content Delivery and Networking

- **Content Delivery Network (CDN)**: Geographically distributed servers speed up web content delivery.
- **AWS CloudFront**: AWS's CDN, using edge locations to deliver data closer to users.
- **AWS Outposts**: AWS hardware deployed on-premises, essentially a mini AWS region in your building.

### VPC (Virtual Private Cloud)

- **VPC**: Logically isolates a section of your AWS resources.
- **Subnets**: IP address ranges within a VPC, grouping resources together (public or private subnets).
- **Internet Gateway**: Public entry point to a VPC.
- **Virtual Private Gateway**: Allows secure connections from specific private networks.

### Security

- **Network Access Control List (ACL)**: Controls access to subnets.
- **Security Group**: Stateful firewall controlling instance-level security.

---

## Common AWS Services and Concepts

|**Service/Concept**|**Description**|
|---|---|
|**Amazon CloudFront**|Reduces network latency.|
|**AWS EC2**|Virtual server in the AWS Cloud.|
|**S3 Glacier Deep Archive**|Lowest cost storage class in Amazon S3.|
|**AWS EFS (Elastic File System)**|Scalable, cloud-native file storage.|
|**Edge Locations**|Data centers that deliver content faster to users.|
|**AWS Organizations**|Manages multiple AWS accounts.|
|**AWS Shield**|Protects against DDoS attacks.|
|**IAM (Identity and Access Management)**|Manages user permissions and access to AWS services.|
|**AWS CloudTrail**|Logs and tracks user activity and API calls.|
|**AWS Key Management Service (KMS)**|Manages encryption and decryption of data.|
|**AWS Lambda**|Run code without provisioning servers.|
|**AWS SageMaker**|Simplifies development and deployment of machine learning models.|
|**AWS Snowball**|Transfers large amounts of data to and from the cloud.|
|**AWS Cost Explorer**|Visualizes and manages AWS costs.|
|**AWS Marketplace**|Allows listing and selling software on AWS.|

---

## Key AWS Exam Questions

- **Which service reduces network latency?**
    - Amazon CloudFront
- **Which Amazon S3 storage class has the lowest cost?**
    - S3 Glacier Deep Archive
- **What is AWS EFS?**
    - AWS Elastic File System
- **What are Edge Locations?**
    - Data centers that deliver content faster to users.
- **Who is responsible for managing storage and databases in AWS Cloud?**
    - AWS
- **What is an IAM Policy?**
    - A document that customizes user permissions for AWS services and resources.
- **What does AWS Shield protect from?**
    - DDoS attacks.
- **What is AWS Lambda?**
    - A service that lets you run code without thinking about servers.

---


- **AWS CloudTrail** captures API calls and tracks all user actions within your AWS account.
- **CloudWatch** monitors your AWS resources and can create automatic alarms for performance or cost optimization.

