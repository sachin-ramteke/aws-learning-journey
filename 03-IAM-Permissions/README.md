# 🔐 Project 03: Identity & Access Management (AWS IAM)

## 📌 Project Overview
Implemented the **Principle of Least Privilege (PoLP)** by configuring non-root IAM user credentials, custom console authentication endpoints, and AWS Managed Permission Policies to isolate developer actions from full administrative privileges.

---

## 🏗️ Security Concepts & Architecture
* **Principle of Least Privilege (PoLP):** Granted strictly necessary read-only permissions instead of administrative privileges to reduce security risks.
* **Separation of Duties:** Differentiated root account owner capabilities from day-to-day developer responsibilities.
* **IAM Policy Enforcement:** Configured managed read-only policies (`AmazonEC2ReadOnlyAccess` and `AmazonS3ReadOnlyAccess`) to restrict resource creation, deletion, and administrative service access.

---

## 🛠️ Step-by-Step Implementation

### 1. User Provisioning
* Created IAM user: `developer-sachin`.
* Enabled AWS Management Console access with custom password credentials.
* Generated isolated console sign-in URL via AWS Account ID (`525426878514`).

### 2. Policy Assignment
* Applied AWS Managed Policies directly:
  * `AmazonEC2ReadOnlyAccess`
  * `AmazonS3ReadOnlyAccess`

### 3. Verification & Access Testing
* **Read Access Validation:** Signed in as `developer-sachin` in a private browser session. Confirmed read visibility of active EC2 key pairs/security groups and S3 bucket contents (`sachin-ramteke-static-website-2026`).
* **Restriction Enforcement:** Tested unauthorized endpoints by accessing the IAM Dashboard. Verified real-time enforcement of `Access Denied` policy barriers across `iam:GetAccountSummary`, `iam:ListMFADevices`, and `iam:ListAccessKeys`.

---

## Key Learnings
* Understanding the security risks of operating with root account credentials.
* How IAM policy evaluation engines grant or deny actions across AWS services.
* Validating multi-tenant permissions through isolated user console sessions.
* 
