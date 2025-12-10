---
title: "System Architecture & Authentication Flow"
date: 2025-12-09
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

{{% notice note %}}
📋 **Overview:** This section describes the high-level architecture of the Aurora system and the authentication flow using Google OAuth 2.0 integrated with Amazon Cognito.
{{% /notice %}}

# 1. High-Level System Architecture

The **Aurora** system is built entirely on a **Serverless architecture** on AWS, optimizing both scalability and operational cost.  
It integrates with **Google Cloud Platform** to provide a seamless Single Sign-On (SSO) experience via Google authentication.

![Aurora Architecture Diagram](/AWS/images/2-Proposal/aws.jpg)  

### Main Components:

1. **Frontend (Client):**  
   A Web App (SPA) where users interact with the system, view schedules, and create tasks.

2. **Authentication Layer:**  
   * **Google Cloud Project:** Provides OAuth 2.0 Client ID/Secret to authenticate Gmail users.  
   * **Amazon Cognito:** Acts as the federated Identity Provider (IdP), managing the User Pool and issuing temporary AWS credentials to the Frontend.

3. **Backend Logic (Compute):**  
   * **AWS Lambda:** Hosts business logic functions (Create Event, Update Tasks, Trigger Email Notifications).

4. **Database:**  
   * **Amazon DynamoDB:** Stores Events and Daily Worklogs.  
     Uses `UserId` as the Partition Key to isolate each user's data securely.

5. **Notification Service:**  
   * **Email Sending Logic:** Triggered by Lambda when a new event is created or when the scheduled time arrives.  
     Sends HTML-formatted emails using SES or a custom Email API.

---

# 2. Authentication Flow

This flow ensures that only authenticated users can access their personal data.  
Aurora uses **Cognito Federated Identities** combined with **Google OAuth 2.0**.

### Step-by-step Process:

1. **User Login:**  
   The user clicks **“Sign in with Google”** on the Frontend.

2. **Google OAuth:**  
   The user is redirected to Google’s login page.  
   After a successful login, Google returns an **Id Token (JWT)**.

3. **Token Exchange:**  
   The Frontend sends the `Id Token` to **Amazon Cognito**.

4. **Verification & Session Handling:**  
   Cognito validates the Token with Google. If the token is valid:  
   * Cognito creates/updates the corresponding user profile in the User Pool.  
   * Cognito returns **temporary AWS credentials** (Access Key, Secret Key, Session Token) to the Frontend.

5. **Authorized Requests:**  
   The Frontend uses these credentials to access API resources (via API Gateway or directly invoking Lambda/DynamoDB through AWS SDK) with permissions defined in IAM Roles.

---

# 3. Data Flow: Creating an Event & Sending Email Notifications

When a user creates a new event (e.g., “Team Meeting at 9:00 AM”), the data flow proceeds as follows:

1. **Frontend → API Request:**  
   The frontend sends a POST request containing the event details to the API endpoint.

2. **AWS Lambda Trigger:**  
   The Lambda function is invoked and performs:  
   * Input validation  
   * Writing event data to **DynamoDB** (Table: `AuroraEvents`)

3. **Email Notification Trigger:**  
   * After writing to DynamoDB, Lambda triggers the email-sending logic.  
   * The system generates an HTML email body.  
   * The Email Service (SES/Gmail API/Resend) sends the message to the user’s inbox.

{{% notice tip %}}
💡 **Highlight:** Integrating Google Login eliminates the need for users to manage an additional password, while benefiting from Google’s built-in two-factor authentication for enhanced security.
{{% /notice %}}
