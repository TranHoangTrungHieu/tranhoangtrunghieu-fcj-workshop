---
title: "Send Reminder (Notification)"
date: 2025-12-09
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

{{% notice warning %}}
🔔 **Function:** This function is designed to run on a schedule (e.g., every 5 minutes using EventBridge Scheduler). It scans the database for events happening within the next 15 minutes and sends reminder emails via a third-party API.
{{% /notice %}}

# Step 1: Create Lambda Function

This function requires a slightly longer execution time since it needs to scan the database and wait for responses from the email API, so we will increase the Timeout.

1. **Function name:** `sendReminder`
2. **Runtime:** Node.js 18.x

> **Illustration:**
>
> ![Screenshot: Create SendReminder Function](images/lambda-reminder-create.png)  
> *Figure 5.4.3.1: Configuring the background job Lambda function.*

---

# Step 2: Configure IAM Role (Full Access to Events)
**JSON Policy:**

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
                "arn:aws:logs:ap-southeast-1:080563425614:log-group:/aws/lambda/sendReminderLambda:*"
            ]
        }
    ]
}
```
## Step 3: Implementation Code (Node.js)
Return to the Lambda Function interface, where we will write Node.js code to scan for upcoming events and send reminder emails via a third-party API.
After completing the code, click **Deploy** to save it.