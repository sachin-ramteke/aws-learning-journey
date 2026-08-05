# 📊 Project 05: Amazon CloudWatch (Monitoring & Alarms)

## 📌 Project Overview
Implemented proactive infrastructure monitoring for EC2 instance workloads using **Amazon CloudWatch** metrics, automated thresholds, and **Amazon SNS (Simple Notification Service)** email alert delivery.

---

## 🏗️ Architecture & Configuration
* **Monitored Resource:** EC2 Instance (`prod-web-server-01` / `i-04e11e4afe93f1909`).
* **Metric:** `CPUUtilization` (Percentage).
* **Evaluation Period:** 5-minute average.
* **Alarm Threshold:** Static threshold `> 70%`.
* **Notification System:** Amazon SNS Topic integrated with email subscription endpoints.

---

## 🛠️ Step-by-Step Implementation

### 1. Metric Selection & Alarm Trigger Definition
* Navigated to the CloudWatch Alarms console in `ap-south-1` (Mumbai).
* Selected `CPUUtilization` per-instance metric for the target web server.
* Defined static rule: Trigger alarm state whenever `CPUUtilization` exceeds **70%**.

### 2. Amazon SNS Integration
* Created/Linked SNS Notification Topic (`Default_CloudWatch_Alarms_Topic`).
* Subscribed admin email endpoint (`ramteke347@gmail.com`) to receive automated alerts upon alarm state changes.

---

## Key Learnings
* Tracking real-time resource usage using CloudWatch Metrics.
* Automating operational observability through customizable Alarm thresholds.
* Routing incident notifications securely using Amazon SNS.
* 
