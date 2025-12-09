---
title: "Frontend & API Gateway"
date: 2025-12-09
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

{{% notice info %}}
🌐 **Architecture:** We will build a standard secure system: Frontend (Amplify) -> API Gateway (with Cognito authentication) -> Lambda Backend.
{{% /notice %}}

# Connection Model

To ensure security and centralized management, the Frontend is not allowed to call Lambda directly. Instead, we use **Amazon API Gateway**.

Workflow:
1. **Deploy:** The ReactJS Frontend is hosted on **AWS Amplify**.
2. **Authenticate:** Users log in via Google/Cognito and receive an `IdToken`.
3. **Request:** The Frontend sends a request to **API Gateway** with the `Authorization Header` containing the Token.
4. **Authorize:** API Gateway verifies the Token with Cognito. If valid -> forwards the request to Lambda.
5. **Execute:** Lambda executes the logic and returns the result.
