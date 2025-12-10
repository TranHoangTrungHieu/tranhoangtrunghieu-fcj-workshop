---
title: "Event CRUD (Event Handler)"
date: 2025-12-09
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

{{% notice info %}}
📅 **Function:** This function handles all Create, Read, Update, and Delete (CRUD) operations for the user's schedules/events.
{{% /notice %}}

# Step 1: Create Lambda Function
* **Function Name:** `auroraTimeEvent`
* **Runtime:** Node.js 18.x
* **Description:** API for handling CRUD operations for the Events table.

> **Image:**
> ![Screenshot: Create Aurora_EventHandler Function](/AWS/images/5-Workshop/lambdaEvent.png)

# Step 2: Configure IAM Role (Full Access to Events)
We need to grant full read/write permissions on the `events` table.

**JSON Policy (CloudWatch Logs permissions):**
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "logs:CreateLogGroup",
            "Resource": "arn:aws:logs:ap-southeast-1:080563425614:*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "logs:CreateLogStream",
                "logs:PutLogEvents"
            ],
            "Resource": [
                "arn:aws:logs:ap-southeast-1:080563425614:log-group:/aws/lambda/auroraTimeEvent:*"
            ]
        }
    ]
}

** JSON Policy (CRUD permissions for DynamoDB events table)
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "AllowCRUDOnEventsTable",
			"Effect": "Allow",
			"Action": [
				"dynamodb:PutItem",
				"dynamodb:GetItem",
				"dynamodb:UpdateItem",
				"dynamodb:DeleteItem",
				"dynamodb:Query"
			],
			"Resource": "arn:aws:dynamodb:ap-southeast-1:080563425614:table/events"
		}
	]
}
```
# Step 3: Processing code (Node.js)
Back to the Lambda Function interface, we will write Node.js code to process CRUD operations.
> **Hình ảnh:**
> ![Screenshot: Create code](/AWS/images/5-Workshop/codeEvent.png)
After completing, click **Deploy** to save.