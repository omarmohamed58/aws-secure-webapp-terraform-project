
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

