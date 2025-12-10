---
title: "CRUD Todo (Tasks)"
date: 2025-12-09
weight: 1
chapter: false
pre: " <b> 5.4.2. </b> "
---

{{% notice info %}}
📅 **Function:** This function handles all Create, Read, Update, and Delete (CRUD) operations for the user's task list.
{{% /notice %}}

# Step 1: Create Lambda Function
* **Function name:** `auroratimeTodo`
* **Runtime:** Node.js 18.x
* **Description:** API that handles CRUD operations for the Todo table.

> **Image:**
> ![Screenshot: Create Aurora_EventHandler](/AWS/images/5-Workshop/lambdaTodo.png)

# Step 2: Configure IAM Role (Full Access to Todo)
We need to grant full CloudWatch and DynamoDB access to the `todo` table.

**JSON Policy (CloudWatch Logs):**
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
                "logs:PutLogTodo"
            ],
            "Resource": [
                "arn:aws:logs:ap-southeast-1:080563425614:log-group:/aws/lambda/auroraTimeTodo:*"
            ]
        }
    ]
}
```json
** JSON Policy (CRUD permissions for DynamoDB todo table)
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "AllowCRUDOnTodoTable",
			"Effect": "Allow",
			"Action": [
				"dynamodb:PutItem",
				"dynamodb:GetItem",
				"dynamodb:UpdateItem",
				"dynamodb:DeleteItem",
				"dynamodb:Query"
			],
			"Resource": "arn:aws:dynamodb:ap-southeast-1:080563425614:table/todo"
		}
	]
}
```
# Step 3: Implement the Logic (Node.js)
Return to the Lambda Function interface and begin writing your Node.js code to handle the CRUD operations.
> **Hình ảnh:**
> ![Screenshot: Create code](/AWS/images/5-Workshop/codeTodo.png)
After completing, click **Deploy** to save your changes.