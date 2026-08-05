# 🚀 AWS Auto Scaled Web Server Deployment (Project 06)

This project demonstrates the end-to-end architecture, deployment, and troubleshooting of a highly available web server infrastructure in AWS. The deployment utilizes a custom Virtual Private Cloud (VPC), dynamic Auto Scaling Groups (ASG), custom Security Groups, and an Apache (`httpd`) web server hosted on Amazon Linux 2023.

---

## 📐 Architecture Overview

* **VPC:** Custom Virtual Private Cloud (`custom-vpc-project04-vpc`)
* **Subnets:** Public Subnet (`custom-vpc-project04-subnet-public1-ap-south-1a`) with Public IPv4 Auto-assignment
* **Internet Gateway:** Attached to VPC and configured in public route table (`custom-vpc-project04-rtb-public`)
* **Compute:** EC2 Instances (`t3.micro`) managed via an Auto Scaling Group (`web-server-asg`)
* **OS:** Amazon Linux 2023
* **Web Server:** Apache (`httpd`)
* **Security:** Custom Security Group (`web-server-custom-sg`) allowing HTTP (Port 80) & SSH (Port 22)

---

## 🛠️ Step-by-Step Deployment Steps

### Step 1: Infrastructure & Network Configuration
1. Created custom VPC and public subnet with Internet Gateway routing.
2. Verified public route table association (`0.0.0.0/0` routed to `igw`).
3. Created security group `web-server-custom-sg` (`sg-0a6d46337dcd0269c`) with inbound rules:
   * **HTTP (Port 80):** `0.0.0.0/0`
   * **SSH (Port 22):** `0.0.0.0/0`

### Step 2: Auto Scaling Group Deployment
1. Configured Launch Template with Amazon Linux 2023 AMI (`t3.micro`).
2. Deployed Auto Scaling Group (`web-server-asg`) inside the target public subnet.
3. Automatically provisioned running instance `i-0fbibcc774b801560e` with public IP `13.207.186.56`.

### Step 3: Server Configuration via Terminal
Connected via **EC2 Instance Connect** and executed the following system setup:

```bash
# 1. Update system packages
sudo dnf update -y

# 2. Install Apache web server
sudo dnf install httpd -y

# 3. Enable and start Apache service
sudo systemctl start httpd
sudo systemctl enable httpd

# 4. Create custom landing page
echo "<h1>Welcome to Auto Scaled Web Server</h1>" | sudo tee /var/www/html/index.html
