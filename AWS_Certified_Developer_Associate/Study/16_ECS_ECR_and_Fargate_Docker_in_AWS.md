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

Task definitions are metadata in JSON form to tell ECS how to run a Docker container

It contains crucial information, such as:

- Image Name
- Port Binding for Container and Host
- Memory and CPU required
- Environment variables
- Networking information
- IAM role
- Logging configuration (ex CloudWatch)

Can define up to 10 containers in a Task Definition

Load Balancing (EC2 Launch Type)

we get a Dynamic Host Port Mapping if you define only the container port in the task definiton

The ALB finds the right port on your EC2 Instances

You must allow on the EC2 intance's Security Group any port from the ALB's Security Group

Loading Balancing (Fargate)

Each task has a unique private IP

Only define the container port (host port is not applicable)

Example)

- ECS ENI security Group
  : Allow port 80 from the ALB
- ALB Security Group
  : Allow port 80/443 from web

One IAM Role per Task Definition

: 특정 Task 에 IAM Role을 부여하여 가령 S3에 접근할 수 있게 한다던지, 혹은 DynamoDB에 접근할 수 있게 한다던지 하는 권한을 부여해준다

Environment Variables

- Hardcoded : URLs
- SSM Parameter Store : sensitive variables (API Keys, shared configs)
- Secrets Manager : sensitive variables (DB Password)

Environment Files (bulk) - Amazon S3

Data Volumnes (Bind Mounts)

Share data between multiple containers in the same Task Definition

Works for both EC2 and Fargate tasks

EC2 Tasks : using EC2 instance storage

- Data are tied to the lifecycle of the EC2 instance

Fargate Tasks : using ephemeral storage

- Data are tied to the container using them
- 20 GiB - 200 GiB (default 20GiB)

Use Cases:

- Share ephemeral data between multiple containers
- "Sidecar" container pattern, where the "sidecar" container used to send metrics/logs to other destination (separation of concerns)

## Amazon ECS Task Definitions - Hands On

## Amazon ECS - Task Placements

## Amazon ECR - Hands On
