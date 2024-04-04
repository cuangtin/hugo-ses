---
title : "Sending Bulk Email with Templates"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 6.3 </b> "
---

In this lab, we will learn how to send bulk emails using Amazon SES and personalized email templates created in previous labs. Sending bulk emails with templates helps save time and effort while ensuring a consistent brand image across all your email communications.
{{% notice note %}}
This lab can only be done using the Amazon SES API and not in the Amazon SES console.
{{% /notice %}}

#### Step 1: Preparing the bulk email data
To send bulk emails, you first need to prepare the data containing the recipients' information and the template data. Create a JSON file named `bulk_email_data.json` with the following sample data:
```
{
  "FromEmailAddress": "sender@example.com",
  "DefaultContent": {
    "Template": {
      "TemplateName": "AWSomeNewsletterTemplate",
      "TemplateData": "{\"name\": \"Subscriber\", \"interest_area\": \"Technology\",\"amazonSESUnsubscribeUrl\": \"https://example-unsubscribe.com\"}"
    }
  },
  "BulkEmailEntries": [
    {
      "Destination": {
        "ToAddresses": ["recipient1@example.com"]
      },
      "ReplacementEmailContent": {
        "ReplacementTemplate": {
          "ReplacementTemplateData": "{\"name\": \"John Doe\", \"interest_area\": \"Technology\",\"amazonSESUnsubscribeUrl\": \"https://example-unsubscribe.com\"}"
        }
      }
    },
    {
      "Destination": {
        "ToAddresses": ["recipient2@example.com"]
      },
      "ReplacementEmailContent": {
        "ReplacementTemplate": {
          "ReplacementTemplateData": "{\"name\": \"Jane Smith\", \"interest_area\": \"Health\",\"amazonSESUnsubscribeUrl\": \"https://example-unsubscribe.com\"}"
        }
      }
    }
  ]
}
```
Replace the email addresses and other details with your actual recipient email addresses and information.
{{% notice warning %}}
Since [subscription option](https://catalog.us-east-1.prod.workshops.aws/workshops/e4a4aa26-fb17-45eb-9edf-77b7f8b6035f/en-US/lab-4/lab-4-4/) and [list management option](https://catalog.us-east-1.prod.workshops.aws/workshops/e4a4aa26-fb17-45eb-9edf-77b7f8b6035f/en-US/lab-4/lab-4-3/) are not yet supported with Amazon SES bulk templated email call, you'd have to manage your preference center externally and dynamically populate the URL for the amazonSESUnsubscribeUrl variable.
{{% /notice %}}

#### Step 2: Sending a bulk email using the email template
To send a bulk email using the "AWSomeNewsletterTemplate" created in the previous labs, use the following AWS CLI command:
```
aws sesv2 send-bulk-email --cli-input-json file://bulk_email_data.json
```
This command sends the personalized email template to all the recipients specified in the `bulk_email_data.json` file.

### Conclusion
In this lab, we have learned how to send bulk emails using Amazon SES and personalized email templates. We prepared the bulk email data containing recipients' information and template data and then sent a bulk email using the send-bulk-email command. By sending bulk emails with templates, you can scale your email marketing efforts and reach a larger audience while maintaining consistency in your email communications.
