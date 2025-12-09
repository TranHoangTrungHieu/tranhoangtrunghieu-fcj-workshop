---
title: "Week 11 Worklog"
date: "2025-09-09T19:53:52+07:00"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives

* Implement core backend components for Aurora Time (Cognito, DynamoDB, Lambda, API Gateway).  
* Build a working Proof of Concept (POC) for authentication and event management.  
* Set up email reminder workflow using EventBridge + SES.  
* Estimate total system cost for deployment.

---

### Tasks Completed This Week

| Day | Task | Start Date | Completion Date | Reference |
|-----|------|-------------|-----------------|-----------|
| **Mon** | - Set up Amazon Cognito User Pool and configure sign-up / sign-in flow.<br>- Test authentication using the Hosted UI and verify ID/Access tokens.<br>- Document how the backend will read user claims for authorization. | 24/11/2025 | 24/11/2025 | Proposal – Cognito & Authentication |
| **Tue** | - Create initial DynamoDB tables (Users, Events, Reminders).<br>- Test basic CRUD operations via Console and AWS CLI.<br>- Validate the partition key design and identify potential hot-partition risks. | 25/11/2025 | 25/11/2025 | Proposal – DynamoDB Data Model |
| **Wed** | - Build backend POC: API Gateway + Lambda functions (CreateEvent, GetEvents).<br>- Connect Lambda with DynamoDB using IAM roles and least-privilege policies.<br>- Test full workflow: HTTP → API Gateway → Lambda → DynamoDB. | 26/11/2025 | 26/11/2025 | Proposal – Serverless Architecture |
| **Thu** | - Configure EventBridge rule + Lambda + SES to send scheduled reminder emails.<br>- Verify SES identities and sending limits.<br>- Successfully send a test reminder email using the POC workflow. | 27/11/2025 | 27/11/2025 | Proposal – EventBridge & SES |
| **Fri** | - Use AWS Pricing Calculator to estimate monthly operational cost for Aurora Time (API Gateway, Lambda, DynamoDB, Amplify, S3, CloudFront, Cognito, SES, EventBridge, CloudWatch).<br>- Finalize cost table for the proposal. | 28/11/2025 | 28/11/2025 | Proposal – Infrastructure Cost Estimate |

---

### Week 11 Achievements

* Successfully implemented the core authentication flow using Amazon Cognito.  
* Designed and deployed DynamoDB tables with correct key structure and access patterns.  
* Built a functional backend prototype using API Gateway + Lambda integrated with DynamoDB.  
* Implemented an automated email reminder system using EventBridge and SES.  
* Produced a detailed AWS cost estimation for the complete serverless architecture.  
* Prepared a stable backend foundation for full integration with the frontend in Week 12.

---
