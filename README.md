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



AWS CLI Profiles


AWS CLI with MFA
- To use MFA with the CLI, you must create a temporary session
- To do so, you must run the STS GetSessionToken API call 


AWS SDK Overview
- without using CLI
You can use an SDK
Official SDKs are Java, .Net, Node, Php, python, go, ruby, c++
Defualt resion us-east-1

Exponential Backoff & Service Limit Increase
- API Rate Limits : 
	 - DescribeInstances API for EC2 has a limit of 100 calls per seconds
	 - GetObject on S3 has a limit of 5500 GET per second per prefix
	 - For Intermittent Errors: implement Exponential Backoff
	 - For Consistenet Errors: request an API throttling limit increase

- Service Quotas(Service Limits)
	- Runnig On-Demand Standard Instance: 1152 vCPU
	- You can request a service limit increase by opening a ticket
	- You can request a service quota increase by using the Service Quotas API

Exponential Backoff (any AWS service)
	- If you get ThrottlingExcption intermittently, use exponentail backoff
	- Retry mechanism already included in AWS SDK API calls
	- Must implement yourself if using the AWS API as-is or in specific cases
		- Must only implement the retries on 5XX server errors and throttling
		- Do not implement on the 4XX client errors

AWS Credentials Provider & Chain

The CLI will look for credentials in this order

1. Command line options: --region, --output, and --profile
2. Environment variable: AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, and AWS_SESSION_TOKEN
3. CLI credentials file
4. CLI configuration file
5. Container credentials

AWS Credentials Scenario
: An application deployed on an EC2 instance is using enviornment variables with credentials form an IAM user to call the Amazon S3 API
The IAM user has S3FullAccess permissions
The application only uses one S3 bucket, so according to best practives: 
	- An IAM Role & EC2 Instance Profile was created for the EC2 instance
	- The Role was assigned the minimum permissions to access that one S3 bucket

The IAM Instance Profile was assigned to the EC2 instance, but it still had access to all S3 buckets. Why?
- the credentials chain is still giving priorities to the environment variables.

AWS Credentials Best Practices

- Overall, NEVER EVER STORE AWS CREDENTIALS IN YOUR CODE
- Best practice is for credentials to be inherited from the credentials chain

If using working within AWS, use IAM Roles
	=> EC2 Instances Roles for EC2 Instance
	=> ECS Roles for ECS tasks
	=> Lambda Roles for Lambda functions

If working outside of AWS, use environmnet variables / named profiles

AWS Signature v4 Signing (Sigv4)


Signing AWS API requests

When you call the AWS HTTP API, you sign the request so that AWS can identify you, using your AWS credentials (access key & secret key)

You should sign an AWS HTTP request using Signature v4 (SigV4)



CloudFront - Caching & Caching Policies

- The cache lives at each CloudFront Edge Location
- CloudFront identifies each object in the cache using the Cache Key (see next slide)
- You want to maximize the Cache Hit ratio to minimize requests to the origin
- You can invalidate part of the cache using the CreateInvalidation API


What is CloudFront Cache Key?
- A unique identifier for every object in the cache
- By default, consists of hostname + resource portion of the URL 
- If you have an application that serves up content that varies based on user, device, language, location
- You can add other elements (HTTP headers, cookies, query strings) to the Cache Key using CloudFront Cache Policies

CloudFront Policies - Cache Policy

Cache based on: 
	- HTTP Headers: None - Whitelist
	- Cookies: None - Include All-Except - All
	- Query Strings: None - Whitelist - Include All-Except - All

Contorl the TTL (0 seconds to 1 year), can be set by the origin using the Cache-Control header, Expires header

All HTTP headers, cookies, and query strings that you include in the Cache Key are automatically included in origin requests

Cache Policy HTTP Headers
	- None 
		- Don't include any headers in the Cache Key (except default)
		- Headers are not forwarded (except default)
		- Best caching performance

	- Whitelist
		- only specified headers included in the Cache key
		- Specified headers are also forwarded to Origin
		
Origin Request Policy

- Specify values that you want to include in origin requests without including them in the Cache Key (no duplicated cached content)

- You can include: 	
	- HTTP headers: None - Whitelist - All viewer headers options
	- Cookies: None - Whitelist - All
	- Query Strings: None - Whitelist - All

Ability to add CloudFront HTTP headers and Custom Headers to an origin request that were not included in the viewer request.

CloudFront - Cache Behaviors
- Configure different settings for a given URL path pattern
- Example: one specific cache behavior to images/*.jpg files on your origin web server
- Route to different kind of origins/origin groups based on the content type or path pattern
	/images/*
	/api/*
	/* (default cache behavior)


CloudFront - Caching & Caching Invalidations - Hands On


CloudFront - Signed URL / Cookies

You want to distribute paid shared content to premium users over the world
We can use CloudFront Signed URL / Cookie. We attach a policy with: 
	- Includes URL expiration
	- Includes IP ranges to access the data from
	- Trusted Signers (Which AWS accounts can create signed URLs)

Signed URL = access to individual files (one signed URL per file)
Signed Cookies = access to multiple files (one signed cookie for many files)


CloudFront Signed URL : 
	- Allow to a path, no matter the origin
	- Account wide key-pair, only the root can manage it
	- Can filter by IP, path, date, expiration
	- Can leverage caching features

S3 Pre-Signed URL: 
	- Issue a request as the person who pre-signed the URL
	- Users the IAM key of the signing IAM principal
	- Limited Lifetime

CloudFront - Signed URL - Key Groups + Hands On

Two types of singers: 
	- Either a trusted key group (recommended)
		- Can leverage APIs to create and rotate keys(and IAM for API security)
	
	- An AWS Account that contains a CloudFront Key Pair
		- Need to manage keys using the root account and the AWS console
		- Not recommended because you shouldn't use the root account for this
	
In your Cloud Front distribution, create one of more trusted key groups
 
You generate your own public / private key 
	 - The private key is used by your applications (e.g. EC2) to sign URLs
	 - The public key (uploaded) is used by CloudFront to verify URLs


CloudFront - Advanced Concepts



CloudFront - Real Time Logs


















