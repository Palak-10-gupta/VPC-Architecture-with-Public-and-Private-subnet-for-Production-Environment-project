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

<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/architecture.336532010-e6b4e573-d8a9-42f0-90bc-90c7497d4aa1.png" alt="Architecture Diagram" width="700"/>
</p>

---

## ⚙️ Step 1: VPC & Subnet Configuration

### VPC Creation
- **CIDR block:** `10.0.0.0/16`  
- Deployed across **two Availability Zones** for redundancy

### Subnets
- **Public Subnets:** `10.0.1.0/24` and `10.0.2.0/24`  
- **Private Subnets:** `10.0.3.0/24` and `10.0.4.0/24`  

### Internet Gateway & Routing
- Public subnets → Internet Gateway  
- Private subnets → NAT Gateway  

<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/createdVPC.png" alt="Created VPC Architecture" width="650"/>
</p>


***Resource Map***

<sup>Two public Subnets connected to the Internet Gateway</sup>
<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/img1.png" alt="VPC Architecture Preview" width="650"/>
</p>


<sup>1st Private Subnet connected to NAT Gateway of 1st public Subnet</sup>
<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/img2.png" alt="Private Subnet 1 connected to NAT Gateway" width="650"/>
</p>


<sup>2nd Private Subnet connected to NAT Gateway of 2nd public Subnet</sup>
<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/img3.png" alt="Private Subnet 2 connected to NAT Gateway" width="650"/>
</p>


---

## 📈 Auto Scaling Group

The **Auto Scaling Group (ASG)** ensures high availability and dynamic scalability of applications:

- Uses a **Launch Template** (with AMI, instance type, key pair, and user-data)  
- Distributes EC2 instances across multiple Availability Zones (AZs)  
- Scales in/out based on **CloudWatch Alarms & policies**

## 🛠️ Step 2: Creating an Auto Scaling Group

### 🔹 Amazon EC2 Auto Scaling
Amazon EC2 Auto Scaling helps maintain application availability by automatically adding/removing EC2 instances based on defined scaling policies.  

- **Dynamic Scaling** → adjusts to real-time demand  
- **Predictive Scaling** → provisions capacity proactively  
- **Fleet Management** → replaces unhealthy instances  

<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/CreateASG.png"  alt="Amazon EC2 Auto Scaling" width="700"/>
</p>

---

### 📝 A. Creating the Launch Template

**1. Selecting AMI (Ubuntu Latest Version)**  
<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/chooseAMI.png" alt="Launch Template AMI" width="650"/>
</p>

**2. Setting Key Pair**  
<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/keypair.png" alt="Launch Template Key Pair" width="650"/>
</p>

**3. Configuring Security Group**  
Allow SSH + Custom TCP (Port 8080) to enable application access.  

<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment
    project/main/assets/securitygroup.png" alt="Security Group Config" width="650"/>
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/img4.png" alt="Security Group Ports" width="650"/>
</p>

---

### 📝 B. Creating the Auto Scaling Group

**1. Selecting the Launch Template**  
<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/ASG.png" alt="ASG Launch Template" width="650"/>
</p>

**2. Configuring VPC & Subnets**  
Attach the ASG to **private subnets** across multiple AZs for redundancy.  

<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/ASG1.png" alt="ASG VPC Setup" width="650"/>
</p>

---

### ✅ Result

After creating the Auto Scaling Group:  
- Two EC2 instances were launched in **both private subnets** across the two AZs.  
- Health checks ensure replacement of unhealthy instances automatically.  

<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/ASG2.png" alt="Final ASG Instances" width="650"/>
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/ASG3.png" alt="Private Instances After ASG" width="650"/>
</p>

---

## 🔒 Step 3: Bastion Host Setup
- Deployed in **Public Subnet**  
- Used to SSH into private instances securely  
- Security Group allows only **whitelisted IPs** (e.g., your laptop IP)  
- **Key-based authentication** enabled

  <p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/bastionhost.jpg" alt="Bastion Host Architecture" width="650"/>
</p>


**Steps to Access Private Instance via Bastion Host:**

```bash
# SSH into Bastion Host
ssh -i key.pem ec2-user@<bastion-public-ip>

# From Bastion, SSH into Private Instance
ssh -i key.pem ec2-user@<private-ip>

---

## ⚡ Step 4: Load Balancer: Traffic Management and High Availability

The **Application Load Balancer (ALB)** is deployed in the **public subnets** to manage incoming traffic, distributing requests to application servers in the **private subnets**.

### 🔹 Key Features & Use Cases:
- 🌐 **Traffic Distribution**: Routes incoming traffic to multiple application servers, ensuring balanced loads and improved performance.  
- 🏢 **High Availability**: Spans across **two Availability Zones**, rerouting traffic to healthy instances in case of failures.  
- 📈 **Auto Scaling Integration**: Works seamlessly with Auto Scaling Groups to distribute traffic to new instances automatically.  
- 🔒 **Secure Access**: Acts as the internet-facing entry point while keeping private subnet servers isolated.  
- 🔑 **SSL Termination**: Manages SSL certificates for secure communication between clients and the ALB.

<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/img5.jpg" alt="Load Balancer Setup" width="700"/>
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/img6.jpg" alt="Target Group Setup" width="700"/>
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/img7.jpg" alt="ALB Routing" width="700"/>
</p>

---

## 🚀 Step 5: Application Deployment in Private Subnet and Access via Bastion Host

In this project, the **application servers are deployed in private subnets** to ensure isolation and security. The **Bastion Host** in the public subnet acts as a secure gateway for accessing these instances.

### 🔹 Deployment & Access Flow:
1. 🖥️ **Deploying the Application in Private Subnet**  
   - Application servers are hosted in **private subnets** to prevent direct internet exposure.  
   - Servers are configured with Auto Scaling for dynamic resource management.  
   - Only authorized traffic flows through the **ALB**, ensuring security and high availability.

2. 🔑 **Accessing the Private Subnet via Bastion Host**  
   - A **Bastion Host** in the public subnet allows secure SSH access to private servers.  
   - Administrators SSH into the Bastion Host first, then tunnel into private servers.  
   - This method keeps the private subnet secure while enabling controlled administrative access.

<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/dNSname.jpg" alt="DNS Name Display" width="650"/>
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/Palak-10-gupta/VPC-Architecture-with-Public-and-Private-subnet-for-Production-Environment-project/main/assets/output.jpg" alt="Final Output" width="650"/>
</p>

### 🌐 Accessing the Application via DNS:
- Users access the application through the **ALB DNS**.  
- The ALB routes requests to private subnet servers, maintaining **security** and **high availability**.  
- No direct internet exposure for private servers ensures a **production-ready architecture**.

---
