---
title: "Configuring Google Cloud & Amazon Cognito"
date: 2025-12-09
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

{{% notice info %}}
⚙️ **Objective:** Set up a Google Cloud Platform project to obtain OAuth credentials and configure Amazon Cognito User Pool as the centralized identity management system.
{{% /notice %}}

# 1. Configuring Google Cloud Platform (GCP)

To allow users to sign in with Gmail, we first need to create a project on Google Cloud and request OAuth 2.0 credentials.

### Step 1: Create an OAuth Client ID
Go to **Credentials** → **Create Credentials** → **OAuth client ID**.
- **Application type:** Web application  
- **Authorized redirect URIs:** This is the address where Google will return the token after successful authentication. (This value will be obtained from the Amazon Cognito Domain in the next section.)

> **Screenshot:**
>
> ![Screenshot: Creating Client ID and Secret](/AWS/images/5-Workshop/ggAuthen.png)  
> *Figure 5.2.2: Creating OAuth Client ID and Client Secret.*

{{% notice warning %}}
Note: Make sure to save the **Client ID** and **Client Secret** for later use in the Cognito configuration.
{{% /notice %}}

---

# 2. Configuring Amazon Cognito User Pool

After obtaining credentials from Google, proceed to AWS Console to configure a User Pool.

### Step 1: Create User Pool & Identity Provider
In the Amazon Cognito interface, create a new User Pool. Under **Sign-in experience**, select **Federated identity providers** and choose **Google**.

Fill in the **Client ID** and **Client Secret** obtained from Google Cloud.

> **Screenshot:**
>
> ![Screenshot: Configuring Google Identity Provider in Cognito](/AWS/images/5-Workshop/provider.png)  
> *Figure 5.2.3: Entering Google authentication details into Cognito.*

### Step 2: Configure App Client & Domain
Under **App integration**:

1. **Domain:** Create a Cognito Domain. This domain will be used as the *Authorized redirect URI* back in Google Cloud.
2. **App Client Settings:**
   - **Allowed callback URLs:** Your application’s frontend URL.
   - **OAuth 2.0 Grant Types:** Select `Authorization code grant`.
   - **OpenID Connect scopes:** Select `email`, `openid`, `profile`.

> **Screenshot:**
>
> ![Screenshot: Configuring App Client Settings](/AWS/images/5-Workshop/cauhinh1.png)  
>  ![Screenshot: Configuring App Client Settings](/AWS/images/5-Workshop/cauhinh2.png) 
> *Figure 5.2.5: Configuring Redirect URL and OAuth Scopes.*

---

# 3. Testing the Configuration (Hosted UI)

To verify your configuration, open the Cognito-hosted **Hosted UI**.  
If the "Continue with Google" button appears and functions correctly, the setup is successful.

> **Screenshot:**
>
> ![Screenshot: Login screen with Google button](/AWS/images/5-Workshop/UI.png)  
> *Figure 5.2.6: Login interface with Google successfully integrated.*
