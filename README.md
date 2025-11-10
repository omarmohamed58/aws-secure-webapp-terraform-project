
## Overview

This project provisions a secure, modular, and scalable multi-tier web application on AWS using Terraform.  
It follows cloud architecture and security best practices including network isolation, least privilege access, and automated infrastructure deployment.

The solution builds a complete AWS environment consisting of:
- A Virtual Private Cloud (VPC) with public and private subnets across multiple Availability Zones  
- Application Load Balancers (public and internal) for routing traffic  
- EC2 instances for the Nginx proxy and backend application layers  
- Security groups enforcing strict access rules between tiers  
- S3 and DynamoDB for Terraform remote state management  

---

## Architecture

                   +----------------------------+
                   |          Internet          |
                   +-------------+--------------+
                                 |
                         Public Application Load Balancer
                                 |
                       +---------+----------+
                       |                    |
                 Public Subnet A       Public Subnet B
                       |                    |
                  EC2 (Nginx)          EC2 (Nginx)
                       |                    |
                 Internal ALB (Private Layer)
                       |
             +---------+----------+
             |                    |
       Private Subnet A     Private Subnet B
             |                    |
       EC2 (Backend App)     EC2 (Backend App)
             |
       NAT Gateway (for updates)
             |
       Internet Gateway



---

## Features

- Infrastructure as Code using Terraform  
- High availability across multiple Availability Zones  
- Network segmentation with separate public and private tiers  
- Layered security model with isolated traffic flow  
- Remote state management using AWS S3 and DynamoDB  
- Modular structure allowing easy updates and scalability  

---

## Project Structure

aws-secure-webapp-terraform-omar/
├── main.tf
├── provider.tf
├── backend.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
├── modules/
│   ├── vpc/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── subnets/
│   ├── igw/
│   ├── nat_gateway/
│   ├── route_tables/
│   ├── security_groups/
│   ├── ec2_proxy/
│   ├── ec2_backend/
│   ├── load_balancer_public/
│   ├── load_balancer_internal/
│   └── target_groups/
└── scripts/
    ├── setup_proxy.sh
    └── setup_backend.sh

---

## Prerequisites

- AWS account with IAM permissions to create networking and compute resources  
- Terraform v1.5 or higher installed  
- AWS CLI configured with valid credentials  
- SSH key pair for EC2 access  
- S3 bucket and DynamoDB table for Terraform remote state  

---

## Terraform Backend Configuration

terraform {
  backend "s3" {
    bucket         = "omar-terraform-state"
    key            = "webapp/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-locks"
    encrypt        = true
  }
}



## Variables Example

project_name          = "omar-webapp"
region                = "us-east-1"
vpc_cidr              = "10.0.0.0/16"
public_subnets_cidrs  = ["10.0.1.0/24", "10.0.2.0/24"]
private_subnets_cidrs = ["10.0.3.0/24", "10.0.4.0/24"]
instance_type         = "t3.micro"
key_name              = "omar-key"

## Outputs

| Output           | Description                          |
| ---------------- | ------------------------------------ |
| vpc_id           | ID of the created VPC                |
| public_subnets   | IDs of public subnets                |
| private_subnets  | IDs of private subnets               |
| public_ec2_ips   | Public IPs of proxy EC2 instances    |
| private_ec2_ips  | Private IPs of backend EC2 instances |
| public_alb_dns   | DNS name of public load balancer     |
| internal_alb_dns | DNS name of internal load balancer   |

## Security Model
| Layer        | Description                   | Allowed Inbound      |
| ------------ | ----------------------------- | -------------------- |
| Public ALB   | Entry point from the internet | 80/443 from all      |
| Proxy EC2    | Reverse proxy layer           | Public ALB only      |
| Internal ALB | Routes internal traffic       | Proxy EC2 only       |
| Backend EC2  | Application layer             | Internal ALB only    |
| NAT Gateway  | Outbound updates              | Private subnets only |

## Future Enhancements
Add Auto Scaling Groups for proxy and backend tiers
Integrate Route53 for domain-based routing
Configure CloudWatch for metrics, logging, and alerts
Implement a CI/CD pipeline using GitHub Actions
Add a private RDS database for persistent storage

