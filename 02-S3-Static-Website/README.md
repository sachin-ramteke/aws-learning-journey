# 🌐 Project 02: Static Website Hosting on Amazon S3

## 📌 Project Overview
Demonstrated serverless web hosting by deploying a static HTML webpage using **Amazon Simple Storage Service (S3)** without provisioning compute instances or web server software.

---

## 🏗️ Architecture & Concepts
* **Serverless Hosting:** Replaced traditional web servers (like Apache) with S3 storage endpoints.
* **Public Bucket Access:** Configured Block Public Access settings and implemented JSON bucket policies for granular `s3:GetObject` read permissions.
* **AWS CLI Deployment:** Utilized AWS CloudShell to programmatically stage and sync web assets directly into the S3 namespace.

---

## 🛠️ Step-by-Step Implementation

### 1. Bucket Creation
* Provisioned an S3 bucket with globally unique name: `sachin-ramteke-static-website-2026`.
* Selected Region: `ap-south-1` (Asia Pacific - Mumbai).

### 2. Website Configuration
* Enabled **Static Website Hosting** in bucket properties.
* Configured index document: `index.html`.

### 3. Public Permissions & Policy
* Disabled **Block *all* public access**.
* Applied the following bucket policy:
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::sachin-ramteke-static-website-2026/*"
        }
    ]
}
