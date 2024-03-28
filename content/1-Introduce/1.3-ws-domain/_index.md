---
title : "Using the default workshop domain"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 1.3 </b> "
---

#### Important Terminologies

For this workshop, your email domain will be a sub-domain of the workshop's root domain (e.g. sesworkshop.online)). Your email domain will be the {teamindex}.sesworkshop.online (e.g.0.sesworkshop.online or 1.sesworkshop.onnline).You can follow the steps below to confirm that your domain is verified and working properly. During the rest of the workshop, replace example.com with your account's verified domain for any actions.

#### Checking that your email domain is verified

Using the AWS CLI, you can check the status of your email domain by using the command

```
aws sesv2 get-email-identity --email-identity {{Your domain name}}
```

You should get the JSON response that has a key value pair of ` VerifiedForSendingStatus ` as ` true `.

A sample JSON response is provided below:

```
{
    "IdentityType": "DOMAIN",
    "FeedbackForwardingStatus": true,
    "VerifiedForSendingStatus": true,
    "DkimAttributes": {
        "SigningEnabled": true,
        "Status": "SUCCESS",
        "Tokens": [
            "oc4vbmhlp2jdgulaqmj64h4a5ea6rvhi",
            "cw3h654y4ufvu7ux4a2mf2bec3le3sw4",
            "67cc7cuhbidfnrxmaocfq33jtdyutqfi"
        ],
        "SigningAttributesOrigin": "AWS_SES",
        "NextSigningKeyLength": "RSA_2048_BIT",
        "CurrentSigningKeyLength": "RSA_2048_BIT",
        "LastKeyGenerationTimestamp": "2024-03-28T23:15:43.083000+07:00"
    },
    "MailFromAttributes": {
        "BehaviorOnMxFailure": "USE_DEFAULT_VALUE"
    },
    "Policies": {},
    "Tags": [],
    "ConfigurationSetName": "my-first-configuration-set",
    "VerificationStatus": "SUCCESS",
    "VerificationInfo": {
        "LastCheckedTimestamp": "2024-03-28T23:26:44.115000+07:00",
        "LastSuccessTimestamp": "2024-03-28T23:26:44.441000+07:00",
        "ErrorType": "HOST_NOT_FOUND",
        "SOARecord": {
            "PrimaryNameServer": "amalia.ns.cloudflare.com",
            "AdminEmail": "dns.cloudflare.com",
            "SerialNumber": 1
        }
    }
}
```

Otherwise, you can access the [Amazon SES console](https://us-east-1.console.aws.amazon.com/ses/) , click on ` Identities ` on the left sidebar and verify that your domain identity has the identity status reflected as ` Verified `.

![Identity](/images/1-WorkshopDomain/identity.png?featherlight=false&width=70pc)