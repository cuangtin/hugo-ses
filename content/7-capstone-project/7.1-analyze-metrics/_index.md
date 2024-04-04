---
title : "Analyzing Metrics"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 7.1 </b> "
---

## Analyzing Metrics for "Weekly Deals" and "Daily Updates" Campaigns

### Scenario
You were just contacted by the marketing heads of two business units in AWSomeNewsletter: `Health & Wellness` and `Travel Tips`. Each unit has different tracking requirements for their email campaigns:

1. The Health & Wellness group runs Daily Wellness Updates and requires tracking number of opens per campaign to understand the performance of each of their campaigns and see how users are engaging with the content.
2. In conjunction with its partners, the `Travel Tips` group sends out a Weekly Travel Deals to its subscribers. In order to properly track affiliate marketing attribution, they need to be able to track the number of clicks per individual link. A sample HTML template which contains the partner deals are given below:
```
<!DOCTYPE html>
<html>
  <head>
    <title>Travel Tips Weekly Deals</title>
  </head>
  <body>
    <h1>Welcome to Travel Tips Weekly Deals!</h1>
    <p>Check out these amazing travel deals from our partners:</p>
    <ul>
      <li>
        <a href="{{traveldeal1}}">Travel Deal 1</a>
      </li>
      <li>
        <a href="{{traveldeal2}}">Travel Deal 2</a>
      </li>
      <li>
        <a href="{{traveldeal3}}">Travel Deal 3</a>
      </li>
    </ul>
  </body>
</html>
```

**Task**: Configure the SES environment to meet the tracking requirements of each business unit.

**Steps**:

### Health and Wellness Business Unit Configuration
1. Configure the Health & Wellness Configuration Set to track open rates using CloudWatch.
- Set up a CloudWatch event destination and specify a custom dimension to segregate email events by a MessageTag of campaign.
{{% notice tip %}}
In [Lab 4.3](../../4-ManageEnvironment/4.3-event-notification-with-cloudwatch) we've configured a Cloudwatch event destination and set the **configuration set** as the Cloudwatch dimension. What should we change in the command to allow the Health & Wellness configuration set to track Cloudwatch metrics using the `campaign` MessageTag?
{{% /notice %}}

2. Modify the AWS CLI commands for sending the Weekly Deals emails:
- Ensure that the email is sent using the appropriate Configuration Set.
- In the same command, add an option to the command that specify the email will be tagged with the key : value pair of `campaign`. You should send at least two test emails, one should be tagged with a key : value pair of `campaign:January`, the other should be tagged with a key : value pair of `campaign:Februrary`.
- Opens and Clicks tracking is only applicable to HTML emails so make sure that you are not sending plaintext emails.
{{% notice tip %}}
Refer to [send-email](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/sesv2/send-email.html) documentation to know which options should be used to add tags to the sent email. If you are accessing your mailbox from a Web Browser, make sure that you disable the Browser's options to Block Trackers and Ads for your Mailbox as they might interfere with Open/Click Tracking.
{{% /notice %}}

If you're successful, you can go into the [Cloudwatch console](https://console.aws.amazon.com/cloudwatch) and browse to the campaign dimension under AWS:SES namespace to see your new metrics being populated.
<!-- image -->

### Travel Business Unit Configuration
1. Modify the HTML template such that each link is tagged with its corresponding partner name i.e.:

- Travel Deal 1 should be tagged to PartnerA
- Travel Deal 2 should be tagged to PartnerB
- Travel Deal 3 should be tagged to PartnerC

2. Once done, upload the template into Amazon SES under the name `TravelTipsWeeklyDeals`.
{{% notice note %}}
Review [Lab 6.1](../../6-email-templates/6.1-create) on how to upload an HTML template into Amazon SES.
{{% /notice %}}

3. Configure the Travel Tips Configuration Set to track click rates using CloudWatch.

a. Set up a CloudWatch event destination and specify a custom dimension to segregate email events by a LinkTag of `partner`.
{{% notice tip %}}
In [Lab 4.3](../../4-ManageEnvironment/4.3-event-notification-with-cloudwatch) we've configured a Cloudwatch event destination and set the **configuration set** as the Cloudwatch dimension. What should we change in the command to allow the Travel Tips configuration set to track individual link clicks using the `partner` LinkTag?
{{% /notice %}}

4. Test your configuration by sending a few emails with the template and clicking on the links to see click tracking. For your convenience, we've provided a sample CLI call with sample template data so you can quickly send the test email:
```
aws sesv2 send-email \
--from-email-address "sender@example.com" \
--destination '{
  "ToAddresses": [
    "recipient@example.com"
  ]
}' \
--content '{
  "Template": {
    "TemplateName": "TravelTipsWeeklyDeals",
    "TemplateData": "{ \"traveldeal1\": \"https://examplepartnerA.com/deal1\", \"traveldeal2\": \"https://examplepartnerB.com/deal2\", \"traveldeal3\": \"https://examplepartnerC.com/deal3\" }"
  }
}' \
--configuration-set TravelTipsConfigSet
```
{{% notice note %}}
Remember to change the sending and recipient email addresses to the appropriate values.
{{% /notice %}}

5. Go into the [Cloudwatch console](https://console.aws.amazon.com/cloudwatch) and browse to the partner dimension under `AWS:SES` namespace to see your new metrics being populated for each partner's link clicks. You can create a graph with a `Sum` statistic and number metric and see your clicks tracked inside Amazon SES and go into Cloudwatch like below.
<!-- image -->

{{% notice note %}}
It might take some time for the metrics to appear in the CloudWatch console. Be patient and refresh the console after a few minutes if you don't see the metrics immediately.
{{% /notice %}}