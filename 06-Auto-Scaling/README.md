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

Verification & Testing
Local Instance Test:
Verified Apache web server functionality locally using curl:
curl http://localhost
Output: <h1>Welcome to Auto Scaled Web Server</h1>
Public Browser Access:
Navigated to http://13.207.186.56 in the web browser to verify live access over Port 80.

🛠️ Real-World Challenges Faced & Solutions
During the implementation of this project, several cloud networking, shell configuration, and browser security challenges were encountered and successfully resolved.
1. Web Page Connection Timeout (ERR_CONNECTION_TIMED_OUT)
Problem: Accessing the public IPv4 address (http://13.207.186.56) in the browser timed out.
Root Cause:
Apache web server service was not started on launch.
Brave Browser was automatically enforcing HTTPS on raw IP addresses.
Solution: Started Apache via systemctl and disabled Brave Shields / automatic HTTPS upgrades for the public IP.
2. Linux Terminal Command Typo (sudo: dgf: command not found)
Problem: sudo: dgf: command not found when trying to install HTTPD.
Solution: Fixed the typo from dgf to dnf.
3. Bash Shell History Expansion Error (-bash: !: event not found)
Problem: Including an exclamation mark (!) inside double quotes in Bash triggered an error.
Solution: Removed the ! from the HTML string before piping to tee.
4. Network Security Diagnostics
Problem: Systematic validation needed across Security Groups, NACLs, and Route Tables.
Solution: Verified Inbound HTTP (80), Outbound ephemeral response ports on NACL, and Route Table association to the Internet Gateway (igw).
🎯 Key Takeaways
Multi-Layered Cloud Networking: Cloud troubleshooting requires checking all network layers sequentially—Route Tables, Internet Gateways, Security Groups (SGs), and Network Access Control Lists (NACLs).
System Service Verification: Launching an EC2 instance via an Auto Scaling Group is only step one; web server processes like Apache (httpd) must be actively running and enabled via systemctl to serve traffic.
Client-Side Security Behavior: Modern browsers (like Brave) enforce HTTPS by default. When serving HTTP traffic on Port 80 without SSL/TLS (Port 443), client-side HTTPS upgrades can cause artificial connection timeouts.
Automated Web Server Deployment: User Data scripts or custom AMIs are essential in production Auto Scaling Groups to ensure newly launched instances configure their web server environment automatically without manual SSH intervention.
