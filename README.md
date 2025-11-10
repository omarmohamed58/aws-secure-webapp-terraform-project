Got it ✅ Omar — here’s the **full professional `README.md`** again, completely cleaned up with **no terminal commands** anywhere, just the documentation and structure as you requested.
Ready to upload directly to your GitHub repo.

---

````markdown
# 🛡️ AWS Secure Web Application with Terraform  
**Author:** [Omar Mostafa](https://www.linkedin.com/in/omar-mostafa10/)  
**Location:** Cairo, Egypt  

---

## 📖 Overview

This project provisions a **secure, modular, and scalable multi-tier web application** on **AWS** using **Terraform**.  
It implements best practices in **network isolation**, **defense-in-depth security**, and **infrastructure as code (IaC)** design.

The solution builds a full cloud environment that includes:
- A **Virtual Private Cloud (VPC)** with public and private subnets across multiple Availability Zones.  
- **Application Load Balancers (ALBs)** for public and internal traffic routing.  
- **EC2 instances** for Nginx reverse proxy and backend application layers.  
- **Security groups** enforcing least privilege between layers.  
- **S3** and **DynamoDB** as a backend for Terraform remote state management.  

---

## 🏗️ Architecture

```text
                       +----------------------------+
                       |        Internet            |
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
           EC2 (Flask App)       EC2 (Flask App)
                 |
           NAT Gateway (for updates)
                 |
           Internet Gateway
````

---

## ⚙️ Features

* **Infrastructure as Code:** Fully automated environment creation with Terraform.
* **High Availability:** Deployed across two availability zones.
* **Network Segmentation:** Clear separation between public and private tiers.
* **Scalability:** Modular architecture ready for Auto Scaling integration.
* **Security Best Practices:** Layered security groups that isolate each tier.
* **Remote State:** Managed state storage using AWS S3 and DynamoDB.
* **Automated Setup:** EC2 instances automatically install and configure Nginx and the backend app.

---

## 📁 Project Structure

```
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
```

---

## 🧰 Prerequisites

* AWS account with IAM permissions to create VPC, EC2, ALB, and related services.
* Terraform v1.5 or higher installed locally.
* AWS CLI configured with access credentials.
* Existing SSH key pair for EC2 access.
* S3 bucket and DynamoDB table configured for Terraform remote state.

---

## 🔒 Terraform Backend Configuration

```hcl
terraform {
  backend "s3" {
    bucket         = "omar-terraform-state"
    key            = "webapp/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-locks"
    encrypt        = true
  }
}
```

---

## 📦 Variables Example

```hcl
project_name          = "omar-webapp"
region                = "us-east-1"
vpc_cidr              = "10.0.0.0/16"
public_subnets_cidrs  = ["10.0.1.0/24", "10.0.2.0/24"]
private_subnets_cidrs = ["10.0.3.0/24", "10.0.4.0/24"]
instance_type         = "t3.micro"
key_name              = "omar-key"
```

---

## 📤 Outputs

| Output             | Description                          |
| ------------------ | ------------------------------------ |
| `vpc_id`           | ID of the created VPC                |
| `public_subnets`   | IDs of public subnets                |
| `private_subnets`  | IDs of private subnets               |
| `public_ec2_ips`   | Public IPs of proxy EC2 instances    |
| `private_ec2_ips`  | Private IPs of backend EC2 instances |
| `public_alb_dns`   | DNS name of public load balancer     |
| `internal_alb_dns` | DNS name of internal load balancer   |

---

## 🔐 Security Model

| Layer        | Description                   | Allowed Inbound      |
| ------------ | ----------------------------- | -------------------- |
| Public ALB   | Entry point from the internet | 80/443 from all      |
| Proxy EC2    | Reverse proxy layer           | Public ALB only      |
| Internal ALB | Routes internal traffic       | Proxy EC2 only       |
| Backend EC2  | Application layer             | Internal ALB only    |
| NAT Gateway  | Outbound updates              | Private subnets only |

---

## ⚙️ Provisioners

Terraform executes scripts during provisioning to configure Nginx and Flask applications automatically.


## 🧩 .gitignore

```
.terraform/
*.tfstate
*.tfstate.backup
terraform.tfvars
*.pem
```

---

## 🧱 Future Enhancements

* Auto Scaling Groups for proxy and backend tiers
* Route53 domain routing integration
* CloudWatch metrics, logging, and alerts
* Continuous Deployment pipeline with GitHub Actions
* Private RDS database layer for persistence

---




Would you like me to now prepare the **Terraform modules and main files** exactly as described here (ready to push to GitHub)?
```
