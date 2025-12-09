---
title: "Create API Gateway & Authentication"
date: 2025-12-09
weight: 1
chapter: false
pre: " <b> 5.6.1. </b> "
---

{{% notice tip %}}
🛡️ **Goal:** Create an HTTP API to consolidate multiple Lambda functions into a single endpoint and secure it using a Cognito Authorizer.
{{% /notice %}}

# Step 1: Create HTTP API

1. Go to **AWS Console** > **API Gateway**.
2. Choose **HTTP API** (low cost, high performance) > Click **Build**.
3. **API name:** `AuroraAPI`.
4. Click **Next** and leave the Integrations blank (we will add them later).
5. **Stage:** Keep the default `$default` (Auto-deploy). Click **Create**.

> **Illustration:**
> ![Screenshot: Create HTTP API Gateway](images/api-create.png)

# Step 2: Connect Lambda (Integrations)

We need to declare which Lambda functions this API will point to (created in section 5.4).

1. Go to **Integrations** > **Manage integrations** > **Create**.
2. Choose **Lambda function**.
3. Select the function `auroratimeEvent` (or other functions you created).
4. Repeat for other functions (`auroratimeTodo`, etc.).

> **Illustration:**
> ![Screenshot: Create Integration pointing to Lambda](images/api-integration.png)

# Step 3: Create Routes

1. Go to **Routes** > **Create**.
2. Define API paths:
    * `POST /events` -> Select integration `auroratimeEvent`
    * `GET /events` -> Select integration `auroratimeEvent`
    * `POST /todos` -> Select integration `auroratimeTodo`
    * …
    *(Note: Action logic can be handled inside the Lambda code or further divided by more detailed routes.)*

> **Illustration:**
> ![Screenshot: API Routes List](images/api-routes.png)

# Step 4: Configure CORS (Important)

To allow the Frontend (Amplify) to call the API, enable CORS:
1. Go to **CORS**.
2. **Access-Control-Allow-Origin:** `*`.
3. **Access-Control-Allow-Methods:** `GET, POST, PUT, DELETE, OPTIONS`.
4. **Access-Control-Allow-Headers:** `Content-Type, Authorization`.
5. Click **Save**.

> **Illustration:**
> ![Screenshot: Configure CORS for API Gateway](images/api-cors.png)

# Step 5: Configure Authentication (JWT Authorizer)

This step secures the API. Only requests with a Cognito token are allowed.

1. Go to **Authorization** > **Manage authorizers** tab > **Create**.
2. **Authorizer type:** JWT.
3. **Name:** `CognitoAuth`.
4. **Identity source:** `$request.header.Authorization`.
5. **Issuer URL:** `https://cognito-idp.ap-southeast-1.amazonaws.com/ap-southeast-1_TryyHPjm0` (replace with your User Pool ID).
6. **Audience:** 5dct7sk93a0unassp7komfpidq
7. Click **Create**.
8. **Attach Authorizer:** Go back to the **Attach authorizers to routes** tab, select routes (`/events`, `/todos`, …) and assign `CognitoAuth` to them.

> **Illustration:**
> ![Screenshot: Assign JWT Authorizer to Route](images/api-authorizer.png)
