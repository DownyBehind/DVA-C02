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


## CloudFormation - Paramters

Paramter is not just string, You can have constraints and validation

AllowedValues (예제 확인할 것)

NoEcho (예제 확인할 것)


Pseudo Parameter
-> 언제나 쓸 수 있는 Parameter들이 있다.


## CloudFormation - Mappings

Mappings are fixed var within your CloudFormation template

-> 예를 들어 특정 ec2의 id를 매번 Template 코드 내에 쓰는 것은 힘들다.
따라서 일종의 MACRO 처리를 하여서 재사용하게 하는 것이 더 유리하다. 

We use Fn::FindInMap to return a named value from a specific key 
!FindInMap [ MapName, TopLevelKey, SecondLevelKey ]

When youd you use Mappings vs. Paramters? 
- Mappings are great when you know in advance all the values that can be taken and that they can be deduced from variable such as
* Region
* AZ
* AWS Account
* Environmnet (dev vs prod)
* etc

- They allow safer control over the template

- Use parameters when the values are really user specific

## CloudFormation - Outputs & Exports

약간 Mapping이랑 유사한 개념 같은데...

The Outputs section declares optional outputs values that we can import into other stacks (if you export them first!)

You can also view the outputs in the AWS Console or in using the AWS CLI

They're very useful for example if you define a network CloudFormation, and output the variables such as VPC ID and your Subnet IDs

It's the best way to perform some collaboration cross stack, as you let expert handle their own part of the stack 

## CloudFormation - Conditions

Conditions are used to control the creation of resources or outputs based on a condition

## CloudFormation - Intrinsic Functions

Ref : reference

The Fn::Ref function can be leveraged to reference
	- Parameters - returns the value of the parameter
	- Resources - returns the physical ID of the underlying resource (ex. EC2 ID)

The shorthand for this in YAML is !Ref


Fn::GetAtt

returns a value for a specified attribute of this type.

Fn::FindInMap

!FindInMap [MapName, TopLevelKey, SecondLevelKey ]

Fn::ImportValue

Import values that are exported in other stacks
For this, we use the Fn::ImportValue function

Condition Functions (Fn::If, Fn::Not, Fn::Equals, etc...)


Fn::Base64

Convert string to Base64


## CloudFormation - Rollbacks

Stack Creation Fails
- Default : everything rolls back (gets deleted). We can look at the log
- Option to disable rollback and troubleshot what happened

Stack Update Fails
- The stack automatically rolls back to the previous know working state
- Ability to see in the log what happened and error messages

Rollback Failure? Fix resources manually than issue
ContinueUpdateRollBack API from Console

## CloudFormation - Service Role

IAM role that allows CloudFormation to create/update/delete stack resources on your behalf
Give ability to users to create/update/delete the stack resources even if they don't have permissions to work with the resources in the stack

## CloudFormation - Capabilities

CAPABILITY_NAMED_IAM and CAPABILITY_IAM
- Necessary to enable when you CloudFormation template is creating or updating IAM resources (IAM User, Group, Policy, Access Keys, Instance Profile)

CAPABILITY_AUTO_EXPAND
- Necessary when your CloudFormation template includes Macros or Nested stacks (stacks within stacks) to perform dynamic transformations
- You're achknowledging that your template may change before deploying

InsufficientCapabilitiesException
- Exception that will be thrown by CloudFormation if the capabilities haven't been acknowledged when deploying a template (security measure)

## CloudFormation - Deletion Policy

삭제할 때 적용할 정책

Default DeletionPolicy = Delete

* S3 bucket이 empty가 아니면 삭제가 안된다. 

DeletionPolicy = Retain
일부 리소스는 유지한다. 

DeletionPolicy = Snapshot
삭제 하기 전에 스냅샷을 하나 찍는다. 

## CloudFormation - Stack Policy

During a CloudFormation stack update, all update actions are allowed on all resources(default)
A Stack Policy is a JSON document that defines the update actions that are allowed on specific resources during Stack updates

## CloudFormation - Temination Protection



## CloudFormation - Custom Resources

Used to 
- define resources not yet supported by CloudFormation
- define custom provisioning logic for resources can that be outside of CloudFormation(on-premises resources, 3rd party resources)

Defined in the template using
AWS::CloudFormation::CustomResource or 
Custom::MyCustomResourceTypeName (recommended)

How to define a Custom Resource?

- ServiceToken specifies where CloudFormation sends requests to, such as Lambda ARN or SNS ARN (required & must be in the same region)

- Input data parameters (optional)

## CloudFormation - StackSets

Create, update, or delete stacks across multiple accounts and regions with a single operaion/template



# AWS Integration & Messaging: SQS, SNS & Kinesis

Sync Communication : app to app

Async Communicaiton / Event Based : app to queue to app

Sync com has a problem with high traffic

 




























Amazon ECR - Hands On

And everything from Section 17 onwards
