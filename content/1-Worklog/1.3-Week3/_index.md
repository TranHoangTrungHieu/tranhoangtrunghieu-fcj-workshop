---
title: "Week 3 Worklog"
date: "2025-09-09T19:53:52+07:00"
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives

* Strengthen understanding of AWS Database and Compute services.  
* Practice deploying Amazon RDS and implementing EC2 Auto Scaling within the same VPC architecture built in Week 2.  
* Develop the ability to design scalable and highly available cloud infrastructures.

---

### Tasks Completed This Week

| Day | Task | Start Date | Completion Date | Reference |
|-----|------|-------------|-----------------|-----------|
| **Mon** | - Learned foundational concepts of Amazon RDS: DB instances, engines, storage types, Multi-AZ deployments, backups, and database security groups.<br>- Reviewed common RDS use cases in web applications. | 22/09/2025 | 22/09/2025 | https://www.youtube.com/watch?v=TQFwQAre0H4 |
| **Tue** | - Created an RDS database instance inside the same VPC as the Week 2 EC2 web server.<br>- Configured database Security Groups to ensure only the EC2 instance (or application subnet) is allowed to connect. | 23/09/2025 | 23/09/2025 | https://www.youtube.com/watch?v=SlP-KdSs3IM |
| **Wed** | - Studied EC2 Auto Scaling: Launch Templates, Auto Scaling Groups (ASG), scaling policies, and health checks.<br>- Designed a simple scaling policy based on CPU utilization. | 24/09/2025 | 24/09/2025 | https://www.youtube.com/watch?v=hFVYG8WqfU0 |
| **Thu** | - Deployed an Auto Scaling Group across at least two Availability Zones.<br>- Tested scale-out and scale-in behavior by modifying thresholds or generating artificial load. | 25/09/2025 | 25/09/2025 | https://000006.awsstudygroup.com |
| **Fri** | - Attended an AWS event to extend real-world cloud knowledge and stay updated with industry best practices. | 26/09/2025 | 26/09/2025 | — |

---

### Week 3 Achievements

* Gained solid understanding of Amazon RDS and how to choose the right database engine, storage class, and Multi-AZ configuration.
* Successfully deployed an RDS instance and configured secure database access restricted to EC2 within the VPC.
* Understood the architecture of a basic 2-tier application: Web tier (EC2) + Database tier (RDS).
* Built competency in EC2 Auto Scaling, including:  
  * Launch Templates  
  * Auto Scaling Groups  
  * Scaling policies  
  * Health checks  
* Successfully implemented an Auto Scaling Group across multiple AZs to improve availability.
* Validated automatic scale-out/scale-in based on CPU usage.
* Strengthened architectural thinking in building elastic, cost-efficient cloud systems.
* Improved ability to combine multiple AWS services into a cohesive, production-l*
