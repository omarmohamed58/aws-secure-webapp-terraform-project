# AWS Secure Web Application with Terraform (By Omar Mostafa)

This project provisions a **secure, modular, and scalable multi-tier web application** on AWS using Terraform.

It follows best practices in **network isolation**, **defense-in-depth security**, and **infrastructure automation** — fully aligned with AWS architecture standards.

---

## 🏗️ Infrastructure Overview

### 🌍 Networking
- **VPC (10.0.0.0/16)** with two **Availability Zones**.
- **2 Public Subnets** → host Nginx reverse proxy EC2 instances.
- **2 Private Subnets** → host backend web application EC2 instances (Flask or Node.js).
- **Internet Gateway** + **NAT Gateway** for controlled access.
- **Route Tables** for public/private segregation.

### ⚖️ Load Balancers
- **Public Application Load Balancer (ALB)** → entry point for internet traffic.
- **Internal ALB** → routes internal traffic from proxies to backend servers.

### 💻 Compute
- **Proxy Tier (Public)** → EC2 instances with Nginx.
- **Backend Tier (Private)** → EC2 instances running Flask app.

### 🔐 Security
Implements a strict multi-layer security model:
- Public ALB SG → allows 80/443 from internet.
- Proxy SG → allows inbound from Public ALB only.
- Internal ALB SG → allows inbound from Proxy instances only.
- Backend SG → allows inbound from Internal ALB only.

---

## 📁 Project Structure

