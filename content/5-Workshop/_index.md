---
title: "Workshop"
date: 2025-12-09
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

{{% notice info %}}
💡 **Project Information:** Aurora is an event-management and automated notification system built on a Serverless architecture.
{{% /notice %}}

# Project Aurora: Event Management & Automated Notification System

#### Project Overview

**Project Aurora** is a solution that enables users to manage schedules, create important events, and track daily tasks (Daily Worklog).  
A key highlight of the system is its ability to integrate **automated email notifications**, reminding users when an event is about to occur.

This project focuses on solving the problem of creating schedules and delivering reliable notifications without maintaining traditional servers.

Key features and services include:

+ **Amazon Cognito & Google Cloud:** Centralized user identity management with **Google Sign-In (OAuth 2.0)** for secure and simplified authentication.
+ **Event & Task Management:** Built using **Amazon DynamoDB** to store event details and daily task statuses.
+ **Email Notification System:** Integrated with **Resend** to deliver beautiful HTML-formatted emails to users.
+ **Logic Processing:** Implemented with **AWS Lambda** to handle workflow execution whenever a new event is created.

![Aurora Time Platform Architecture](/AWS/images/2-Proposal/aws.jpg)

#### Detailed Sections

1. [System Architecture & Authentication Flow](5.1-Architecture/)
2. [Google Cloud & Amazon Cognito Configuration](5.2-Auth-Setup/)
3. [Database Design (Events & Tasks)](5.3-Database/)
4. [Building API & Email Logic (Lambda)](5.4-Backend-Logic/)
5. [User Interface (Frontend)](5.5-Frontend/)
6. [Final Results & Future Improvements](5.6-Conclusion/)
