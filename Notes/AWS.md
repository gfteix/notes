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




