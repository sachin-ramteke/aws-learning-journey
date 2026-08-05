# 🌐 Project 04: Amazon Virtual Private Cloud (VPC)

## 📌 Project Overview
Designed and deployed a custom, isolated cloud network architecture using **Amazon VPC**, complete with public and private subnets, an Internet Gateway (IGW), and configured route tables to enforce network perimeter security.

---

## 🏗️ Architecture & Networking Design
* **CIDR Block:** `10.0.0.0/16` (65,536 available IP addresses).
* **Public Subnet:** `10.0.0.0/20` — Configured with an Internet Gateway route for public-facing assets (Web Servers). Auto-assign public IPv4 enabled.
* **Private Subnet:** `10.0.16.0/20` — Isolated subnet with no direct inbound/outbound internet access for internal workloads (Databases).
* **Internet Gateway (IGW):** Attached to the VPC to enable IPv4 internet traffic routing.
* **Route Tables:** Configured explicit target routes (`0.0.0.0/0` -> IGW) for the public subnet.

---

## 🛠️ Step-by-Step Implementation

### 1. VPC & Subnet Provisioning
* Initialized custom VPC: `custom-vpc-project04` in `ap-south-1` (Mumbai).
* Provisioned isolated Dual-Subnet structure across Single Availability Zone (`ap-south-1a`).
* Cost Optimization: Set NAT Gateway and VPC Endpoints to `None` to prevent hourly charges.

### 2. Network Routing & Public Access Configuration
* Verified attached Internet Gateway (`igw-0a30d147123c445a5`).
* Modified Public Subnet attributes to automatically allocate public IPv4 addresses to launched EC2 instances.

---

## Key Learnings
* Understanding Classless Inter-Domain Routing (CIDR) block allocation.
* Distinguishing between Public Subnets (IGW routed) and Private Subnets (Isolated/NAT routed).
* Controlling cloud network boundaries and traffic flow via custom Route Tables.
* 
