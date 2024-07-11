# VPC Fundamentals

## VPC, Subnets, IGW and NAT

VPC : private network to deploy your resources (regional resource)

Subnets : allow you to partition your network inside your VPC (Availability Zone resource)

A public subnet is a subnet that is accessible from the internet

A private subnet is a subnet that is not accessible from the internet

To define access to the internet and between subnets, we use Route Tables

Internet Gateways helps our VPC instances connect with the internet

public subnets have a route to the internet gateway

NAT Gateways (AWS-managed) & NAT Instances (self-managed) allow your instances in your Private Subnets to access the internet while remaining private

## NACL, SG, VPC Flow Logs

NACL(Network ACL)

- A firewall which controls traffic from and to subnet
- Can have ALLOW and DENY rules
- Are attached at the Subnet level
- Rules only include IP addresses

Security Groups

- A firewall that controls traffic to and from an ENI / an EC2 Instance
- Can have only ALLOW rules
- Rules include IP addresses and other security groups

VPC Flow Logs

Capture information about IP traffic going into your interfaces:

- VPC Flow Logs
- Subnet Flow Logs
- Elastic Network Interaface Flow Logs

## VPC Peering, Endpoints, VPN

Connect two VPC, privately using AWS' network

Make them behave as if they were in the same network

Must not have overlapping CIDR(IP address range)

VPC Peering connection is not transitive (must be established for each VPC that need to communicate with one another)

VPC Endpoints

Endpoints allow you to connect to AWS Services using a private network instead of the public www network

This gives you enhanced security and lower latency to access AWS services

VPC Endpoint Gateway: S3 & DynamoDB

Site to Site VPN

- Connect an on-premises VPN to AWS
- The connection is automatically encrypted
- Goes over the public internet

Direct Connect(DX)

- Establish a physical connection between on-premises and AWS
- The connection is private, secure and fast
- Goes over a private network
- Takes at least a month to establish

## VPC Cheat Sheet & Closing Comments

VPC : Virtual Private Cloud
Subnet: Tied to an AZ, network partition of the VPC
Internet Gateway: at the VPC level, provide Internet Access
NAT Gateway / Instances: give internet access to private subnets
NACL: Stateless, subnet rules for inbound and outbound
Security Groups: Stateful, operate at the EC2 instance level or ENI
VPC Peering: Connect two VPC with non overlapping IP ranges, non transitive
VPC Endpoints: Provide private access to AWS Services within VPC
VPC Flow Logs: network traffic logs
Site to Site VPN: VPN over public internet between on-premise DC and AWS

## Three Tier Architecture
