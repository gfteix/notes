---
title: AWS Elastic Load Balancer
description:
aliases:
tags:
draft: "true"
created-date: 2025-10-31
---

Elastic Load Balancdf (ELB) automatically manages incoming traffic to your applications in the cloud. It serves as a single front door that receives all incoming requests and distributes them across multiple servers.
These targets include Amazon EC2 instances, containers, and IP addresses. ELB improves overall application availability.


- **Type of Load Balancers**: ELB offers different types of load balancers: Application Load Balancer for web traffic, Network Load Balancer for TCP/UDP traffic, and Gateway Load Balancer for network appliances. Each type serves specific application needs.
- **Listeners**: are processes that check for connection requests using a configured protocol and port. Each load balancer needs at least one listener to accept traffic. Listeners direct connection requests from clients to your targets.
- **Target Group**: Target groups are logical groupings of targets like EC2 instances, IP addresses, or AWS Lambda functions. Target groups receive load balancer traffic and help you manage multiple targets together. ELB can distribute traffic across multiple Availability Zones within your target groups.