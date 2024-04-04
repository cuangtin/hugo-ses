---
title : "Personalizing Email Templates with Dynamic Content"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 6.2 </b> "
---

In this section, we will learn how to personalize the email templates created in the previous part (Lab 5.1) with dynamic content, such as the recipient's name, location, or other attributes. We will use [template data](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/send-personalized-email-api.html) and [replacement tags](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/templates-replacement-tags.html) in Amazon SES to achieve this.
{{% notice note %}}
This lab can only be done using the Amazon SES API and not in the Amazon SES console.
{{% /notice %}}

#### Step 1: Update the HTML email template with replacement tags
Edit the `awesome_newsletter_template.html` file created in the previous section and add replacement tags for personalization. For this example, we will personalize the recipient's name and their interest area.

Update the email template with the following content:
```
<!DOCTYPE html>
<html>
  <head>
    <title>AWSomeNewsletter</title>
    <style>
      body {
        font-family: Arial, sans-serif;
      }
      h1 {
        color: #3e3e3e;
      }
      p {
        font-size: 14px;
      }
      .footer {
        font-size: 12px;
        color: #999999;
      }
    </style>
  </head>
  <body>
    <div style="max-width: 600px; margin: auto;">
      <h1>AWSomeNewsletter: Your Monthly Digest</h1>
      <p>Hello {{name}},</p>
      <p>
        Here's a roundup of the latest news and articles in the
        {{interest_area}}:
      </p>
      <ul>
        <li><a href="#">Article 1: Exciting News in {{interest_area}}</a></li>
        <li><a href="#">Article 2: Developments You Should Know About</a></li>
        <li><a href="#">Article 3: What Experts Are Saying</a></li>
      </ul>
      <p>Stay tuned for more updates next month!</p>
      <p class="footer">
        If you no longer wish to receive these emails, please
        <a href="{{amazonSESUnsubscribeUrl}}">unsubscribe</a>.
      </p>
    </div>
  </body>
</html>
```
We're using **handlebars** {{}} notation to indicate to Amazon SES where the variables need to be substituted. As you can see, we have added the `{{name}}` and `{{interest_area}}` replacement tags to the template. Handlebars notation can also be used to add an unsubscribe link to Amazon SES's built-in subscription management feature, as detailed in [Lab 5.4](../../5-ListAndSubscription/5.4-Subscription%20Management).

#### Step 2: Update the email template in Amazon SES

{{% notice note %}}
If you're using the AWS Cloudshell, you'd need to first remove the previously uploaded file by running the command `rm awesome_newsletter_template.html`. Afterwards, reupload the modified `awesome_newsletter_template.html` file to AWS Cloudshell.
{{% /notice %}}

Unlike [Lab 6.1](../6.1-create) in which you are **creating** a new email template, we want to **update** the existing template in Amazon SES. To do so, run the following command:
```
aws sesv2 update-email-template --cli-input-json "$(printf '{"TemplateName": "AWSomeNewsletterTemplate", "TemplateContent": {"Subject": "AWSomeNewsletter Monthly Digest", "Html": "%s"}}' "$(sed -e ':a' \
-e 'N' \
-e '$!ba' \
-e 's/\n/\\n/g' \
-e 's/"/\\"/g' \
awesome_newsletter_template.html)")"
```

{{% notice note %}}
Note that we are using `update-email-template` instead of `create-email-template` because we're updating an existing email template in Amazon SES.
{{% /notice %}}

#### Step 3: Send a personalized email using the updated template
To send a personalized email using the updated template, run the following command and replace the `sender@example.com` and `recipient@example.com` placeholders with your actual sender and recipient email addresses:
```
aws sesv2 send-email \
  --from-email-address "sender@example.com" \
  --destination '{"ToAddresses":["recipient@example.com"]}' \
  --content '{"Template": {"TemplateName": "AWSomeNewsletterTemplate", "TemplateData": "{\"name\": \"John Doe\", \"interest_area\": \"Technology\"}"}}' \
  --list-management-options '{"ContactListName": "AWSomeNewsletterContactList"}'
```
{{% notice note %}}
We're passing the template data inside the command's `Content.Template.TemplateData` attribute. Also note that for the unsubscribe link to work, we need to pass the `ListManagementOption` into the call. Replace `MyContactList` with the name of the contact list (e.g. AWSomeNewsletterContactList) you created in [Lab 5.2](../../5-ListAndSubscription/5.2-configuration-set-level-suppression). For more on Subscription Management, refer to [Lab 5.4](../../5-ListAndSubscription/5.4-Subscription%20Management).
{{% /notice %}}

Next, run the following command to send the personalized email:
```
aws sesv2 send-email --cli-input-json file://send_data.json
```

<!-- image -->

### Conclusion
We have covered the following topics:

1. **Creating Email Templates**: We learned how to create email templates in Amazon SES using the AWS CLI. This included generating a sample HTML email template relevant to the AWSomeNewsletter use case.
2. **Personalizing Email Templates with Dynamic Content**: We explored how to personalize email templates with dynamic content using handlebar notations. We added placeholders for the recipient's name and interest area, as well as an unsubscribe link using the `{{amazonSESUnsubscribeUrl}}` handlebar notation.
With the knowledge gained from this lab, you should now be able to create and personalize email templates for your own use cases.

In the next lab, [Lab 6.3: Sending Bulk Email with Templates](../6.3-send-bulk), we will dive into how to use the email templates we have created to send personalized emails to multiple recipients at once. This will help you scale your email marketing efforts and increase engagement with a more extensive audience.