---
title: "Week 8 Worklog"
date: "2025-09-09T19:53:52+07:00"
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives

* Finalize business requirements and user stories for the **Aurora Time** scheduling application.  
* Design the end-to-end serverless architecture for authentication, backend APIs, database, and automation workflows.  
* Build the DynamoDB data model and define API contracts for backend development.

---

### Tasks Completed This Week

| Day | Task | Start Date | Completion Date | Reference |
|-----|------|-------------|-----------------|-----------|
| **Mon** | - Refined business requirements for Aurora Time: event management, reminders, authentication, email notifications.<br>- Defined non-functional requirements: latency, scalability, availability, security, cost efficiency. | 03/11/2025 | 03/11/2025 | Proposal – Executive Summary, NFRs |
| **Tue** | - Designed the high-level serverless architecture using API Gateway, Lambda, DynamoDB, EventBridge Scheduler, SES, Cognito, Amplify, and S3/CloudFront.<br>- Created the architecture diagram based on AWS best practices. | 04/11/2025 | 04/11/2025 | Proposal – Solution Architecture |
| **Wed** | - Designed the DynamoDB data model: Users, Events, Reminders tables with appropriate PK/SK values.<br>- Analyzed access patterns: list events by date, event detail retrieval, update/delete operations, user-scoped queries.<br>- Estimated RCU/WCU usage for expected workloads. | 05/11/2025 | 05/11/2025 | Proposal – DynamoDB Modeling |
| **Thu** | - Defined the backend API contract: full list of REST endpoints such as /events, /events/{id}, /reminders.<br>- Documented request/response schemas, validation rules, and error handling formats.<br>- Mapped each API endpoint to its Lambda function and required IAM permissions. | 06/11/2025 | 06/11/2025 | Proposal – API Design & IAM Roles |
| **Fri** | Attended an AWS event and documented insights relevant to serverless design and event-driven architecture. | 07/11/2025 | 07/11/2025 | — |

---

### Week 8 Achievements

* Completed all business requirements and user stories for the Aurora Time application.  
* Designed a **fully serverless architecture**, ensuring:  
  * automatic scaling  
  * high availability  
  * low operational cost  
  * simplified deployment and maintenance  
* Built a well-structured **DynamoDB data model** optimized for real access patterns.  
* Produced a complete **API contract**, enabling seamless coordination between frontend and backend development.  
* Strengthened understanding of AWS services used in the project, including:  
  * Cognito — Authentication  
  * API Gateway — Request routing & API management  
  * Lambda — Business logic  
  * DynamoDB — NoSQL data storage  
  * EventBridge — Scheduling & automation  
  * SES — Email notifications  
  * Amplify/S3/CloudFront — Frontend hosting  
* Prepared for the next phase: implementing Lambda backend functions and building the initial Aurora Time application prototype.

---
