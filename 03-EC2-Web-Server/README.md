 # Project 03: Amazon EC2 Linux Web Server Deployment

## Overview
Successfully provisioned and deployed an Apache HTTP Web Server on an Amazon Linux 2023 EC2 instance within the Asia Pacific (Mumbai) `ap-south-1` region using AWS Management Console and EC2 Instance Connect.

---

## Architecture
```text
[ Web Browser / Internet Client ]
              │
              ▼ (Port 80 - HTTP)
     [ Internet Gateway ]
              │
              ▼
  [ Virtual Private Cloud (VPC) ]
              │
              ▼
   [ Security Group Firewall ]
     ├── Allow SSH (Port 22)
     └── Allow HTTP (Port 80)
              │
              ▼
   [ Amazon EC2 Instance ]
     ├── Type: t3.micro
     ├── OS: Amazon Linux 2023
     ├── Storage: 8 GiB gp3 EBS Root Volume
     └── Web Server: Apache (httpd)
