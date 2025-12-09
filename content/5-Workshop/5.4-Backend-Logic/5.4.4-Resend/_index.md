---
title: "Resend & Route 53 Configuration"
date: 2025-12-09
weight: 1
chapter: false
pre: " <b> 5.4.0. </b> "
---

{{% notice info %}}
📧 **Goal:** Before writing the email-sending logic, we need to verify our domain (Domain Verification) to ensure outgoing emails do not land in Spam. We will connect **Resend** with **AWS Route 53**.
{{% /notice %}}

# Step 1: Add Domain to Resend

1. Go to the [Resend Dashboard](https://resend.com/domains).
2. Click **Add Domain**.
3. Enter your domain: auroratime.click.
4. Select **Region**.
5. Click **Add**. Resend will provide you with three types of DNS records (MX, SPF, DKIM).

> **Illustration:**
> ![Screenshot: DNS Records provided by Resend](images/resend-dns-records.png)

# Step 2: Configure DNS in AWS Route 53

We need to copy the DNS records from Resend and add them to Route 53.

1. Go to **AWS Console** > **Route 53** > **Hosted zones**.
2. Select your domain.
3. Click **Create record**.
4. **Create the MX record (Mail Exchange):**
    * **Record name:** (Leave empty or use the value provided by Resend)
    * **Record type:** MX
    * **Value:** Copy from Resend
5. **Create the TXT records (SPF & DKIM):**
    * Do the same for each TXT record required by Resend.
    * *Note:* If the Record name ends with your domain, in Route 53 you only need to enter the prefix (e.g., `bounces`), because Route 53 will automatically append the domain.

> **Illustration:**
> ![Screenshot: Creating a Record in Route 53](images/route53-create-record.png)

# Step 3: Verify and Get API Key

1. Return to Resend and click **Verify DNS Records**.
2. Wait around 1–5 minutes until the status turns **Verified** (Green).
3. Go to **API Keys** > **Create API Key**.
4. Name your key and select **Sending access**.
5. **Copy and store this API Key securely** (We will use it in the Lambda code in later sections).

> **Illustration:**
> ![Screenshot: Resend showing successful verification](images/resend-verified.png)

{{% notice tip %}}
💡 **Tip:** This DNS configuration improves your domain's reputation, ensuring that system emails from Aurora land in the **Inbox** instead of **Spam**.
{{% /notice %}}
