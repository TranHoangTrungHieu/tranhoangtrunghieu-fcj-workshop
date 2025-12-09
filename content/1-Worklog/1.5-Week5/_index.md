---
title: "Week 5 Worklog"
date: "2025-09-09T19:53:52+07:00"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives

* Understand how AWS Storage Gateway integrates on-premises environments with AWS Cloud storage.  
* Build hands-on experience with S3, EC2 (as gateway host), and Storage Gateway setup.  
* Learn real-world hybrid storage use cases such as backup, archiving, and file caching.

---

## Tasks Completed This Week (AWS Storage Gateway Module)

| Day | Task | Start Date | Completion Date | Reference |
|-----|------|-------------|-----------------|-----------|
| **Mon** | - Learned the fundamentals of AWS Storage Gateway and its 3 gateway types (File, Volume, Tape).<br>- Reviewed hybrid storage use cases and the Storage Gateway lab architecture (EC2 acting as gateway + S3 backend storage). | 13/10/2025 | 13/10/2025 | https://www.youtube.com/watch?v=Je2jPk7HhLQ |
| **Tue** | - Created the required S3 bucket for the Storage Gateway lab.<br>- Configured bucket settings: name, region, encryption, tags. | 14/10/2025 | 14/10/2025 | https://www.youtube.com/watch?v=3vSrTeWroSs |
| **Wed** | - Launched an EC2 instance to host the Storage Gateway appliance.<br>- Configured networking and Security Groups so the instance can securely communicate with S3 and the AWS Storage Gateway service. | 15/10/2025 | 15/10/2025 | https://www.youtube.com/watch?v=xVrhpe8OpVU |
| **Thu** | - Activated the Storage Gateway and connected it with the previously created S3 bucket.<br>- Configured the correct gateway type according to the lab scenario and verified the gateway reached **ACTIVE** state. | 16/10/2025 | 16/10/2025 | https://www.youtube.com/watch?v=Je2jPk7HhLQ |
| **Fri** | - Performed end-to-end validation: mounted file share/volume, tested read/write operations, and verified data synchronization to S3.<br>- Wrote an internal note summarizing how Storage Gateway bridges on-premises storage with AWS cloud workloads. | 17/10/2025 | 17/10/2025 | https://www.youtube.com/watch?v=3Zp9GSMO-VI |

---

### Week 5 Achievements

* Gained a solid understanding of the **AWS Storage Gateway architecture** and its hybrid storage use cases.
* Successfully created an **S3 bucket** to act as backend storage for the lab environment.
* Deployed an **EC2 instance** acting as the Storage Gateway host and configured network access securely.
* Activated and configured the Storage Gateway, ensuring it was properly connected to S3.
* Validated storage operations by performing read/write tests and confirming S3 synchronization.
* Improved understanding of how cloud storage integrates with traditional on-premises environments.
* Strengthened hybrid-cloud architectural skills, preparing for more advanced storage and migration modules.

---
