---
title: Terraform
description:
aliases:
tags:
draft: "true"
created-date: 2025-10-06
---


- Terraform Intro: https://developer.hashicorp.com/terraform/intro

-  Terraform Recommended Practices: https://developer.hashicorp.com/terraform/cloud-docs/recommended-practices

- Terraform AWS Provider resources: https://registry.terraform.io/providers/hashicorp/aws/latest/docs

- Best practices for using Terraform with AWS https://docs.aws.amazon.com/prescriptive-guidance/latest/terraform-aws-provider-best-practices/introduction.html



---


## Notes on how to setup AWS and Terraform

- Install Terraform
- Install AWS CLI
- Get and configure AWS Credentials
	- Make sure to have an AWS user configured
	- Locally, run `aws configure` or `aws configure sso` and follow config steps
- On the root folder, create a `main.tf` file and add the provider
```
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 6.0"
    }
  }
}

provider "aws" {
   profile = "default"
   region = "us-east-1"
}

```
- Run `terraform format` to format terraform files
- Run `terraform init` so terraform downloads the provider
- Create an EC2 Instance
```
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 6.0"
    }
  }
}

provider "aws" {
  profile = "study"
  region = "us-east-1"
}


resource "aws_instance" "app_server" {
  ami = "ami-0360c520857e3138f"
  instance_type = var.ec2_instance_type

  tags = {
    Name = var.instance_name
  }
}
```
- Run `terraform plan` to see the changes
- Run `terraform apply` to apply the changes
- Go to aws console and verify that the instance was created
- Use the data source provider instead of hardcoding the ami
	- You can use `data` blocks to query your cloud provider for information about other resources. This data source fetches data about the latest AWS AMI that matches the filter, so you do not have to hardcode the AMI ID into your configuration. Data sources help keep your configuration dynamic and avoid hardcoded values that can become stale.
	- To get the Owner ID of some ami:
		- Find an example ami on AWS Catalog
		- Run `aws ec2 describe-images --image-ids THE_EXAMPLE_AMI --region THE_REGION --profile YOUR_PROFILE

```
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 6.0"
    }
  }
}

provider "aws" {
  profile = "study"
  region  = "us-east-1"
}


data "aws_ami" "ubuntu" {
  most_recent = true

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd-gp3/ubuntu-noble-24.04-amd64-server-*"]
  }

  owners = ["099720109477"] # Canonical
}

resource "aws_instance" "app_server" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = var.ec2_instance_type

  tags = {
    Name = var.instance_name
  }
}

```

- Run `terraform destroy` to destroy all resources