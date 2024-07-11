# AWS CLI SDK IAM Roles & Policies

## AWS EC2 Instance Metadata (IMDS)

AWS EC2 Instance Metadata(IMDS) is powerful but one of the least known features to developers

It allows AWS EC2 instances to "learn about themselves" without using an IAM Role for that purpose.

You can retrieve the IAM Role name from the metadata, but you CANNOT retrieve the IAM policy

Metadata = Info about the EC2 instance
Userdata = launch script of the EC2 instance

IMDSv2 vs. IMDSv1

IMDSv1 is accessing http://169.254.169.254/latest/mata-data directly

IMDSv2 is more secure and is done in two steps:

    1. Get Session Token (limited validity) - using headers & PUT

    2. Use Session Token in IMDSv2 calls - using headers

## AWS CLI with MFA

- To use MFA with the CLI, you must create a temporary session
- To do so, you must run the STS GetSessionToken API call

## AWS SDK Overview

- without using CLI
  You can use an SDK
  Official SDKs are Java, .Net, Node, Php, python, go, ruby, c++
  Defualt resion us-east-1

## Exponential Backoff & Service Limit Increase

- API Rate Limits :

  - DescribeInstances API for EC2 has a limit of 100 calls per seconds
  - GetObject on S3 has a limit of 5500 GET per second per prefix
  - For Intermittent Errors: implement Exponential Backoff
  - For Consistenet Errors: request an API throttling limit increase

- Service Quotas(Service Limits)
  - Runnig On-Demand Standard Instance: 1152 vCPU
  - You can request a service limit increase by opening a ticket
  - You can request a service quota increase by using the Service Quotas API

Exponential Backoff (any AWS service) - If you get ThrottlingExcption intermittently, use exponentail backoff - Retry mechanism already included in AWS SDK API calls - Must implement yourself if using the AWS API as-is or in specific cases - Must only implement the retries on 5XX server errors and throttling - Do not implement on the 4XX client errors

## AWS Credentials Provider & Chain

The CLI will look for credentials in this order

1. Command line options: --region, --output, and --profile
2. Environment variable: AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, and AWS_SESSION_TOKEN
3. CLI credentials file
4. CLI configuration file
5. Container credentials

AWS Credentials Scenario
: An application deployed on an EC2 instance is using enviornment variables with credentials form an IAM user to call the Amazon S3 API
The IAM user has S3FullAccess permissions
The application only uses one S3 bucket, so according to best practives: - An IAM Role & EC2 Instance Profile was created for the EC2 instance - The Role was assigned the minimum permissions to access that one S3 bucket

The IAM Instance Profile was assigned to the EC2 instance, but it still had access to all S3 buckets. Why?

- the credentials chain is still giving priorities to the environment variables.

## AWS Credentials Best Practices

- Overall, NEVER EVER STORE AWS CREDENTIALS IN YOUR CODE
- Best practice is for credentials to be inherited from the credentials chain

If using working within AWS, use IAM Roles
=> EC2 Instances Roles for EC2 Instance
=> ECS Roles for ECS tasks
=> Lambda Roles for Lambda functions

If working outside of AWS, use environmnet variables / named profiles

## AWS Signature v4 Signing (Sigv4)

Signing AWS API requests

When you call the AWS HTTP API, you sign the request so that AWS can identify you, using your AWS credentials (access key & secret key)

You should sign an AWS HTTP request using Signature v4 (SigV4)
