[[AWS]] [[VPC]]
# 8.1 VPC Introduction
VPC is a virtual data center in the cloud
- Logically isolated part of AWS cloud where you can define your own network
- Complete control of virtual network, including your own IP address range, route table, and network gateways

## Fully customize network

- Web: Public-facing subnet
- Application: Private subnet. Can only speak to web tier and database tier
- Database: Private subnet. Can only speak to application tier
## What can we do with a VPC?

- Launch instances
- Internet gateway
- Custom IP address
- Route tables
- More security control
- Access control lists

## Default VPC vs Custom VPC

### Default

- Default VPC is user friendly
- All subnets in default VPC have a route out to the internet
- Each EC2 instance has both a public and private IP

### Custom

- Fully customizable
- Takes time to set up

## Exam tips

- Think of a VPC as a logical data center in AWS
- Consist of internet gateways (or virtual private gateway), route tables, network access control list, subnets, and security groups
- **1 subnet is always in 1 AZ - You cannot span multiple AZ** 

Popular exam topic:
**What is automatically created when you create a VPC?**
-> Route table, network ACL, security group