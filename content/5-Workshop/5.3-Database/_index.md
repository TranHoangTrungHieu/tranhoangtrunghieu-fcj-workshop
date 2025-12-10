---
title: "Database Design (Events & Tasks)"
date: 2025-12-09
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

{{% notice info %}}
🗄️ **Objective:** Design a NoSQL database using Amazon DynamoDB to store Events and Todo tasks, optimized for fast retrieval and low operational cost.
{{% /notice %}}

# 1. Why Choose Amazon DynamoDB?

With Aurora’s Serverless architecture, **Amazon DynamoDB** is the ideal choice because:

* **Serverless:** No server management required, automatically scales based on workload.
* **High performance:** Low latency (single-digit milliseconds), ideal for real-time UI operations.
* **Flexible (Schemaless):** Easy to add new fields to Event/Todo items without complex migrations like SQL databases.

---

# 2. Schema Design (Data Modeling)

The system follows a **Per-User Isolation** model.  
Every item is associated with a `userId` (extracted from Cognito/Google tokens) to ensure data security.

We will create **three main tables**:

### Table 1: AuroraEvents (Stores calendar events)

This table stores user events, displayed on the calendar and used for notification scanning.

* **Partition Key (PK):** `userId` (String) — User identifier  
* **Sort Key (SK):** `eventId` (String) — UUID of the event

### Table 2: AuroraTasks (Stores daily tasks)

This table stores the user’s Daily Worklog / Todo list.

* **Partition Key (PK):** `userId` (String)  
* **Sort Key (SK):** `todoId` (String) — UUID of the task

### Table 3: users (Stores user information)

This table contains detailed information about each user.

* **Partition Key (PK):** `userId` (String)

---

# 3. Steps to Create Tables on AWS Console

Below are the steps to create tables using the AWS DynamoDB Console.

### Step 1: Create the Events Table

Navigate to **DynamoDB → Tables → Create table**.

* **Table name:** `events`  
* **Partition key:** `userId` (String)  
* **Sort key:** `eventId` (String)

> **Screenshot:**  
> ![Screenshot: Creating AuroraEvents table](/AWS/images/5-Workshop/dbEvent.png)

---

### Step 2: Create the Tasks Table

Repeat the process to create the Tasks table.

* **Table name:** `todo`  
* **Partition key:** `userId` (String)  
* **Sort key:** `todoId` (String)

> **Screenshot:**  
> ![Screenshot: Creating AuroraTasks table](/AWS/images/5-Workshop/dbTodo.png)

---

### Step 3: Create the Users Table

Finally, create the Users table.

* **Table name:** `users`  
* **Partition key:** `userId` (String)

> **Screenshot:**  
> ![Screenshot: Creating Users table](/AWS/images/5-Workshop/dbUser.png)

