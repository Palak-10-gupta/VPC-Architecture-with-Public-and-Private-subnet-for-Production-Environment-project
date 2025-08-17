# VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project
# 🌐 VPC Architecture with Public and Private Subnets

## 📌 Introduction
This project demonstrates how to design and deploy a secure, scalable, and highly available cloud infrastructure on **AWS** using a **Virtual Private Cloud (VPC)**.

The setup follows **AWS Well-Architected Framework** principles, ensuring:
- 🔒 Security by isolating workloads in private subnets  
- ⚡ High availability across multiple Availability Zones (AZs)  
- 📈 Scalability using Auto Scaling Groups  
- 🎯 Controlled access via Bastion Host  

---

## 🏗️ Architecture Overview

### 🔑 Key Components
- **VPC** – Custom Virtual Private Cloud spanning 2 AZs  
- **Public Subnets** – For ALB, NAT Gateway, Bastion Host  
- **Private Subnets** – For application servers & databases  
- **Auto Scaling Group** – Manages EC2 scaling dynamically  
- **Application Load Balancer (ALB)** – Distributes incoming traffic securely  
- **NAT Gateway** – Enables outbound internet from private subnets  
- **Bastion Host** – Secure entry point for administration  

---

## 📊 Architecture Diagram
![Architecture Diagram](https://github.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/architecture.336532010-e6b4e573-d8a9-42f0-90bc-90c7497d4aa1.png)


---
