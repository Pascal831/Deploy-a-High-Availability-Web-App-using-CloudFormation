# ☁️ Udacity Cloud DevOps Project 2: Deploy a High-Availability Web App Using CloudFormation

### 👤 Author: Pascal Egbenda  
> This project showcases the use of **AWS CloudFormation** to automate the deployment of a highly available web application infrastructure across multiple Availability Zones.

---

## 📌 Project Objective

You are tasked with deploying **Udagram**, an Instagram-like application, on AWS using Infrastructure as Code. The application code is hosted in a public S3 bucket and must be deployed securely and reliably to private subnets. This includes setting up:

- VPC and networking components
- Bastion Host for secure access
- Web servers behind an Application Load Balancer
- Auto Scaling for high availability
- IAM roles and security groups

---

## 📈 Project Structure

The project is modularized into three CloudFormation stacks:

### 1. 🛠️ Network Stack
- VPC
- Public and Private Subnets
- Internet and NAT Gateways
- Route Tables

**Deployment Command:**
```bash
./create.sh Network network-infrastructure.yml network-infrastructure-parameters.json
```

---

### 2. 🔐 Bastion Host Stack
- Bastion server in a public subnet for SSH access
- Secure access configured via Security Groups and IAM

**Deployment Command:**
```bash
./create.sh Bastion-Servers Bastion-Host.yml Bastion-Host-parameters.json
```

---

### 3. 🌐 WebApp Stack
- Auto Scaling Group with 4 EC2 instances (2 per Availability Zone)
- Application Load Balancer
- Listener on port 80
- S3 integration to pull web assets
- Health checks and user-data configuration

**Deployment Command:**
```bash
./create.sh WebApp WebApp.yml WebApp-parameters.json
```

---

## 🧾 Key Specifications

- **AMI:** Ubuntu 18.04
- **Instance Type:** 2 vCPUs, ≥4 GB RAM
- **Disk Space:** ≥10 GB
- **Inbound Rules:**
  - Port 80: Load balancer & app servers
  - Port 22: Bastion host (restricted to specific IPs)
- **Outbound Access:** Unrestricted for app instances
- **IAM Role:** S3 access for instances to pull application code
- **Outputs:** Load Balancer Public URL

---

## 🧪 Testing & Troubleshooting

✅ Confirm web app loads via the Load Balancer  
✅ Check `/var/log/cloud-init-output.log` for UserData script output  
✅ Bastion host allows SSH into private subnets  
✅ Validate auto-scaling and load balancing in response to traffic

---

## 📦 Included Helper Scripts

| Script Name         | Description                         |
|---------------------|-------------------------------------|
| `create.sh`         | Creates a new CloudFormation stack  |
| `update.sh`         | Updates an existing stack           |
| `delete-stack.sh`   | Deletes the specified stack         |

---

## 🔥 Bonus Features

- Public Load Balancer URL exported with `http://` prefix
- Bastion host configured in public subnet with limited SSH access
- Web servers deployed in private subnets for enhanced security

---

## 📸 Screenshots Included

- VPC and subnet setup  
- Bastion and WebApp stack creation  
- EC2 instances and target groups  
- Load balancer health checks  
- CloudFormation outputs and parameters  
- Auto Scaling group activity

---

## 🧹 Cleanup

Be sure to delete your stacks using `delete-stack.sh` to avoid ongoing AWS charges.

```bash
./delete-stack.sh WebApp
./delete-stack.sh Bastion-Servers
./delete-stack.sh Network
```

---

## 🧾 Documentation & Resources

- 📄 [Project PDF Report](./Udacity%20Project-2.pdf)
- 🖼️ [Network Diagram (PNG)](./Udacity%20Project-2.png)

---

## 🚀 Conclusion

This project demonstrates how to build a production-ready, automated AWS infrastructure using CloudFormation. It emphasizes modularity, high availability, scalability, and secure access—all critical components for any DevOps or cloud-focused role.
