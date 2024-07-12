# DVA-C02

Study note about AWS Developer - Associate C02

Ultimate AWS Certified Developer Associate 2024 NEW DVA-C02

https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/?couponCode=ACCAGE0923

AWS DVA

B] If you first completed my AWS Certified Solutions Architect course and don't want to re-watch content...

Please watch the following lectures:

Section 7 - AWS Fundamentals: ELB + ASG

Auto Scaling Groups - Instance Refresh

Section 8 - AWS Fundamentals: RDS + Aurora + ElastiCache

ElastiCache Strategies

Amazon MemoryDB for Redis

Section 9 - Route 53

Routing Policy - Traffic Flow & Geoproximity Hands On

Section 10 - VPC Fundamentals

VPC Fundamentals - Section Introduction

VPC, Subnets, IGW and NAT

NACL, SG, VPC Flow Logs

VPC Peering, Endpoints, VPN, DX

VPC Cheat Sheet & Closing Comments

Three Tier Architecture

Section 12 - AWS CLI, SDK, IAM Roles & Policies

AWS EC2 Instance Metadata

AWS EC2 Instance Metadata - Hands On

AWS CLI Profiles

AWS CLI with MFA

AWS SDK Overview

Exponential Backoff & Service Limit Increase

AWS Credentials Provider & Chain

AWS Signature v4 Signing

Section 15 - CloudFront

CloudFront - Caching & Caching Policies

CloudFront - Cache Behaviors

CloudFront - Caching & Caching Invalidations - Hands On

CloudFront - Signed URL / Cookies

CloudFront - Signed URL - Key Groups + Hands On

CloudFront - Advanced Concepts

CloudFront - Real Time Logs

Section 16 - ECS, ECR & Fargate - Docker in AWS

Amazon ECS - Rolling Updates

Amazon ECS Task Definitions - Deep Dive

Amazon ECS Task Definitions - Hands On

Amazon ECS - Task Placements

Amazon ECR - Hands On

And everything from Section 17 onwards









# ECS, ECR & Fargate - Docker in AWS

## Amazon ECS - Rolling Updates

When updating from v1 to v2, we can control how many tasks can be started and stopped, and in which order
-> 업데이트가 필요할 때, 기존 버전으로 운영되는 ECS 중에서 최소 사용량만 빼고 나머지 종료 후, 종료된 수 만큼 업데이트 처리함

ECS Rolling Update - Min 50%, Max 100%

Starting Number of tasks : 4 

Stop 2 tasks and update 2 tasks from v1 to v2

and Stop another 2 tasks(v1) and update these 2 tasks from v1 to v2

finally all tasks are v2


ECS Rolling Update - Min 100%, Max 150%

Starting Number of tasks : 4 

Add 2 v2 Tasks 

and Stop 2 tasks(v1) and update these 2 tasks from v1 to v2

and Stop another 2 tasks(v1) and update these 2 tasks from v1 to v2

finally all tasks are v2


## Amazon ECS Task Definitions - Deep Dive




## Amazon ECS Task Definitions - Hands On



## Amazon ECS - Task Placements



## Amazon ECR - Hands On
