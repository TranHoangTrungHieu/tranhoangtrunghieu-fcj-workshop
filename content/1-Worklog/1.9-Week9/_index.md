---
title: "Week 9 Worklog"
date: "2025-09-09T19:53:52+07:00"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives

* Begin implementing the backend foundation for the Aurora Time application.  
* Set up authentication, database tables, API endpoints, and event-driven email reminders.  
* Validate cost estimation for all AWS services involved.

---

### Tasks Completed This Week

| Day | Task | Start Date | Completion Date | Reference |
|-----|------|-------------|-----------------|-----------|
| **Mon** | - Set up a basic Cognito User Pool and tested sign-up/sign-in through hosted UI.<br>- Inspected ID/Access tokens, reviewed claims, and documented how APIs will extract user identity. | 10/11/2025 | 10/11/2025 | Proposal – Cognito Authentication |
| **Tue** | - Created initial DynamoDB tables based on the Week 8 data model (Users, Events, Reminders).<br>- Executed CRUD operations in Console and CLI.<br>- Verified PK/SK design and identified potential hot-partition risks for future scaling. | 11/11/2025 | 11/11/2025 | Proposal – DynamoDB Data Model |
| **Wed** | - Built a minimal POC integrating API Gateway → Lambda → DynamoDB.<br>- Implemented 1–2 endpoints (CreateEvent, ListEvents).<br>- Successfully tested end-to-end flow using sample requests. | 12/11/2025 | 12/11/2025 | Proposal – Serverless Architecture |
| **Thu** | - Implemented EventBridge + Lambda + SES prototype for scheduled reminders.<br>- Verified SES email sending, configured identities, and reviewed SES sandbox limitations.<br>- Validated reminder trigger flow end-to-end. | 13/11/2025 | 13/11/2025 | Proposal – EventBridge & SES |
| **Fri** | - Used AWS Pricing Calculator to estimate monthly cost for Aurora Time backend and frontend services: Lambda, API Gateway, DynamoDB, Cognito, SES, EventBridge, S3, CloudFront, Amplify, CloudWatch.<br>- Documented projected cost based on expected usage. | 14/11/2025 | 14/11/2025 | Proposal – Infrastructure Cost Estimate |

---

### Week 9 Achievements

* Successfully established **authentication** for Aurora Time using Cognito User Pools with working sign-up/sign-in flows.  
* Created operational **DynamoDB tables**, validated the data model, and performed CRUD operations via Console and CLI.  
* Developed the first working **API endpoints** for the backend using API Gateway + Lambda + DynamoDB.  
* Built a functional **reminder prototype** using EventBridge + Lambda + SES, demonstrating the event-driven approach.  
* Completed a detailed **cost estimation** for all AWS services used in the project.  
* Gained hands-on experience integrating multiple AWS serverless components into a unified backend workflow.  
* Prepared for Week 10, where more advanced backend features and production-ready logic will be implemented.

---
