---
title: "Proposal"
date: "2025-09-09T19:53:52+07:00"
weight: 2
chapter: false
pre: "<b> 2. </b>"
---

## **Aurora Time**

---

### **Executive Summary**
This proposal presents the implementation plan for **Aurora Time**, a time-management application built on AWS.  
The goal is to provide a simple, intuitive, and cost-efficient scheduling tool for individual users.

Aurora Time leverages **Serverless** and **Managed Services** on AWS to achieve scalability, high reliability, and cost optimization — delivering **rapid return on investment (ROI)** by eliminating infrastructure maintenance overhead.

---

### **Problem Statement**

#### **Current Problems**
Users struggle to manage their personal schedules because information is scattered across many tools (notes, phones, various apps).  
Existing solutions are often overly complex, business-oriented, and not suited for individual use.

**Aurora Time** provides a **centralized, minimalistic, and intuitive** solution that helps users easily manage habits and personal events.

#### **Proposed Solution**
Aurora Time uses **Amazon S3** and **CloudFront** to store and distribute the web application, and **AWS Amplify** for quick deployment.  
**Amazon API Gateway** and **AWS Lambda** handle backend CRUD operations, while **DynamoDB** provides fast and stable data storage.  
**Amazon Cognito** handles user authentication, and **EventBridge** & **SES** send automated reminders.

**Key Features:**
- Intuitive scheduling interface  
- Custom reminders  
- Extremely low cost  

---

### **Benefits and Return on Investment (ROI)**
Aurora Time helps users save time, reduce scattered scheduling, and increase productivity.  
- **Infrastructure cost:** $16 – $50/month (~$192 – $600/year)  
- **ROI:** Under 6 months  
- **Advantages:** No servers needed, ultra-low cost, highly scalable  

---

### **Solution Architecture**
Aurora Time applies an **AWS Serverless architecture** that allows flexible scaling from a single user to millions.  
Requests are received by **Amazon API Gateway**, processed by **AWS Lambda**, and stored in **DynamoDB**.  
**EventBridge** schedules and triggers reminders, **AWS Amplify** hosts the frontend, and **Cognito** provides security.

![AWS Serverless Architecture for Aurora Time](/images/2-Proposal/aurora-architecture.jpeg)

---

### **AWS Services Used**

| AWS Service | Function |
|--------------|------------|
| **AWS Lambda** | Handles CRUD business logic and reminders. |
| **Amazon API Gateway** | Provides secure RESTful APIs. |
| **Amazon DynamoDB** | Stores scheduling, event, and user data. |
| **Amazon S3 & CloudFront** | Stores and distributes the frontend content. |
| **Amazon EventBridge** | Schedules and triggers automated events. |
| **Amazon SES** | Sends reminder emails to users. |
| **AWS Amplify** | Hosts and manages the frontend. |
| **Amazon Cognito** | Secure user authentication and management. |

### **Technical Implementation Plan**

1. **January – Research & Architecture Design:**  
   DynamoDB modeling, Serverless architecture (API Gateway, Lambda, EventBridge).  
2. **January – POC & Cost Estimation:**  
   AWS Pricing Calculator, testing Cognito + DynamoDB.  
3. **February – System Optimization:**  
   Tune Lambda (timeout, memory), optimize DynamoDB RCU/WCU.  
4. **February–March – Development & CI/CD:**  
   Build Lambda functions, set up CodePipeline + CodeBuild, develop React UI, Beta testing.  

---

### **Estimated Infrastructure Cost**

| Service | Description | Monthly Cost (USD) |
|----------|--------|--------------------|
| AWS Amplify | Static web hosting | 0.35 |
| S3 | Static files & backup | 0.05 |
| CloudFront | CDN (20GB) | 1.70 |
| API Gateway | 30,000 requests | 0.11 |
| Lambda | 1M requests (free tier) | 0.00 |
| DynamoDB | 1GB data (free tier) | 0.11 |
| Cognito | <1000 users | 0.00 |
| SES | 500 emails/month | 0.05 |
| EventBridge | 100k events | 0.10 |
| CloudWatch Logs | 1GB logs | 0.10 |
| CI/CD Pipeline | 20 builds | 0.00 |

👉 **Total Estimated Cost:** ~ $16 – $50/month (~$192 – $600/year)

---

### **Risks & Mitigation**

| Risk | Impact | Probability | Mitigation |
|--------|------------|-----------|-------------|
| Network outage | Medium | Medium | Use cache & CDN (CloudFront). |
| DynamoDB failure | High | Medium | Conduct POC & load testing. |
| Cost overrun | Medium | Low | Set up AWS Budgets alerts. |
| EventBridge/Lambda failure | High | Low | Monitor via CloudWatch & retry logic. |

---

### **Expected Outcomes**
- Simple, intuitive scheduling with automated reminders.  
- Stable, low-cost, scalable serverless system.  
- Full deployment during internship with automated CI/CD.  
