---
title : "Email Identities"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

### Email Identities

You'll need to have a verified identity to be able to send email through Amazon SES. For this next part of the lab, you can verify your own email address, which will act as the "From" address for your company newsletter.

![SES Console](/images/2/1/0001.png?featherlight=false&width=70pc)
![Create Identity](/images/2/1/0002.png?featherlight=false&width=70pc)

{{% notice note %}}
If you're sending to a different email address and you're in a sandbox SES environment, you'd need to also verify the recipient address because sandbox environment will only allow sending to verified email addresses.
{{% /notice %}}

1. Open your terminal or command prompt and ensure that you have the AWS CLI installed and configured with the necessary permissions to access Amazon SES.
2. Enter the following command to verify an email address as a verified identity:

```
aws sesv2 create-email-identity --email-identity example@example.com
```

Replace `example@example.com` with the email address you want to verify, which will be used as the "From" address for your company newsletter.

### Verifying Email Identities
1. If you have enabled email receiving for the email address you are verifying, you will receive an email with a verification link. Click the link to complete the verification process.

2. To check the verification status of an email address, enter the following command:
```
aws sesv2 get-email-identity --email-identity example@example.com
```
This will return a JSON object with the verification status of the specified email address, similar to below:

```
{
    "IdentityType": "EMAIL_ADDRESS",
    "FeedbackForwardingStatus": true,
    "VerifiedForSendingStatus": true,
    "DkimAttributes": {
        "SigningEnabled": false,
        "Status": "NOT_STARTED",
        "SigningAttributesOrigin": "AWS_SES",
        "NextSigningKeyLength": "RSA_1024_BIT"
    },
    "MailFromAttributes": {
        "BehaviorOnMxFailure": "USE_DEFAULT_VALUE"
    },
    "Policies": {},
    "Tags": [],
    "ConfigurationSetName": "my-first-configuration-set",
    "VerificationStatus": "SUCCESS",
    "VerificationInfo": {}
}
```