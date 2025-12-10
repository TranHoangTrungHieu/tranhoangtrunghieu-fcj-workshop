---
title: "Backend-Logic"
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

{{% notice info %}}
🛡️ **Goal:** Build a Serverless Backend following a 4-step workflow: Create Function → Configure Role → Grant Database Permissions → Implement Logic (Connect to DB & Call Third-Party Email API).
{{% /notice %}}

# Step 1: Initialize the Lambda Function

First, we create a new Lambda function that will contain the processing logic.

1. Go to **AWS Console** > **Lambda** > **Create function**.
2. **Function name:** *(enter your function name)*.
3. **Runtime:** Choose **Node.js 18.x** (or 20.x).
4. **Architecture:** x86_64.
5. Keep the remaining settings as default and click **Create function**.

> **Illustration:**
>
> ![Screenshot: Lambda Function Initialization Screen](/AWS/images/5-Workshop/lambda.png)  
> *Figure 5.4.1: Creating the Backend processing Lambda function.*

---

# Step 2: Add Policies to the Lambda (Execution Role)

When the function is created, AWS automatically generates a basic IAM Role.  
We need to access this Role and add permissions for writing to the Database.

1. In the Lambda function page, switch to the **Configuration** tab.
2. Select **Permissions** on the left panel.
3. Click the Role name under **Execution role** to open it in the IAM Console.

> **Illustration:**
>
> ![Screenshot: Accessing Execution Role from Lambda](/AWS/images/5-Workshop/role.png)  
> *Figure 5.4.2: Accessing the IAM Role for permission configuration.*

---

# Step 3: Add Policies for Database Access

Since we use a third-party Email service (called via a normal HTTP API), we **do not** need SES permissions.  
We only need to grant Lambda permissions to work with **DynamoDB**.

1. In the Role’s **Permissions** tab, click **Add permissions** > **Create inline policy**.
2. Switch to the **JSON** mode.
3. Click **Next**, name the policy `AuroraDB_Access_Policy`, and then click **Create policy**.
4. Review your Permissions list to ensure the Role now has access to DynamoDB.
![Screenshot: Truy cập vào add policy từ Lambda](/AWS/images/5-Workshop/permission.png)
---

# Step 4: Write the Lambda Function Code

Return to the Lambda Function interface and begin writing your Node.js code.
![Screenshot: Truy cập vào để viết code](/AWS/images/5-Workshop/code.png)
Once completed, click **Deploy** to save and apply the changes.
