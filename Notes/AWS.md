---
title: AWS
description: 
aliases: 
tags:
  - tech
draft: "true"
created-date: 2025-05-03
---

# AWS Account Setup

- Setup MFA for root user
- Create billing alerts
- Set up an Admin User Account using IAM Identity Center 
	- Create User
	- Go to AWS Accounts -> Click on the root account -> Assing users/group -> Select the created User -> Assing Permission sets -> Create a Permission set and asign
	- Add MFA to it
	- Go to Dashboard -> Edit the Dashboard URL 
- Stop using root user and use admin account now


# AWS CLI Setup
- Install AWS CLI
- Run `aws configure sso` and follow config steps
- Set the profile name with something easy to use such as 'admin' or 'sandbox' 
- Run the aws cli commands with the `--profile admin` at the end
- `aws s3 ls --profile admin`
- To login in the sso profile `aws sso login --profile admin`


---

# Services


## VPC
- When you create an aws account, aws automatically generates a VPC for you
- RFC 1918 -> Private IP Range, it will not conflict with no ip adress on the internet
- Do not use the same range for different vpc to not overlap ips

To connect vpc with other vpcs, there are two options:
- VPC peering
- Transit Gatway

## Subnets
- You need subnets to put resources in VPCs
- Are subdivisions of the ip ranges

Rule of Thumb for subnet sizing

| Purpose                 | Suggested size                |
| ----------------------- | ----------------------------- |
| Small test/dev subnet   | `/26` (64 IPs)                |
| Medium app subnet       | `/24` (256 IPs)               |
| Large / scalable subnet | `/23` or `/22` (512–1024 IPs) |


> For picking an IP range in general (192.168.x.y, 10.x.y.z, etc.) review RFC1918 for valid IP ranges, and pick one that isn't conflicting with anything on your corporate network or people's home networks - otherwise VPNs and VPC peering won't work.


## Route table

- contains rule for which package goes where
- your vpc has a default route table
- you can create and **assign** different route tables to different **subnets**
- the route table belongs to a vpc, and we associate subnets with route tables



## Network Access Control List
A layer of protection for the subnet (statless)
A virtual "firewall"

## Security Groups
- NACL protects the subnet, but after something enter the subnet we have security groups.
- Like a virtual firewall that protects an ec2 instance.
- It is stateful.


## Internet Gateway
Allow connecting the VPC to the external network (Internet)


## Nat Gateway
Network address translation service

We can use so instances in private network can connect with services outside the vpc but external services can not initiate a connection with this private server

- Create Nat Gateway on public subnet
- Use a private route table to route to the nat gateway - allowing our private subnet to reach out to the internet.


## Transit Gateway


## EC2


## EBS


## GuardDuty
Amazon GuardDuty is a threat detection service


## Amazon Elastic Load Balancer (ELB) 
Distributes incoming network traffic across multiple servers, preventing any single resource from being overwhelmed

## Amazon Auto Scaling Group (ASG) 
Adjusts the number of EC2 instances based on the current demand. It provides elasticity, allowing the application to adapt to changes in traffic patterns





## [[AWS SQS]]


## Step Functions

AWS Step Functions can coordinate the distributed components of your application and keep the need for orchestration out of your code. It automatically launches and tracks each step, and can retry steps when there are errors. 


While using Step Functions for orchestrating, you have different enterprise messaging patterns that you can implement

- Sequential Tasks: Iterate through each state in the state machine throug a sequential order
- Conditional Choice: Add branching logic to the state machine
- Looping Tasks: Iterate your state machine task a specific number of times
- Try/catch/finally: Deals with errors and exceptions automatically based on your defined business logic
- Parallel: Used to create parallel branches in your state machine



Step Machines can be used for tasks that requires human intervation by using a callback integration pattern.


Step Functions Express Workflows are an alternative to the Standard Workflows. Express Workflows are designed for high-volume, short-duration use cases.

See https://docs.aws.amazon.com/step-functions/latest/dg/choosing-workflow-type.html


## Webhook
User defined http callback

- Trusted: you own both sides and can define a secure integration. Webhook is established outside of the process
- Untrusted: Webhook established during the registration process, or required as part of the api data


For trusted clients we can use SNS to set up an HTTP subscription that notified the client using a webhook.


## App Sync
is a fully managed GraphQL service with real-time data synchronization and offline programming features.
With AWS AppSync, clients can automatically subscribe and receive status updates as they occur.

## Kinesis
Streaming service to ingest and process large volumes of data in near-real time

Producers add rdata ecords to the stream and Consumers get records and process them

Kenesis services scales horitzontally by adding shards. Data capacity is configured by the number of shards configured in the stream.