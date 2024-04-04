---
title : "Diagnosing and Fixing Issues"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 7.2 </b> "
---

### Scenario
After configuring the tracking information for the two business units, the head of marketing for the `Travel Tips` group has modified the template they provided to you in [Scenario 1](../7.1-analyze-metrics) to include HTML and CSS formatting to make it more beautiful. However, they mentioned that their subscribers are complaining of the email not rendering as expected in some email clients. They also wanted to modify the template such that they don't have to list all the travel deals one by one. The template should pull from the template data and dynamically populate the travel deals based on the user. Lastly, as the IT manager for the email environment, the marketing department has asked you

Task: You are provided with the following email template for AWSomeNewsletter's `Weekly Deals` campaign. Your goal is to troubleshoot the rendering failure and provide an alternative to make the email render the same on all email clients. You should also modify the template so that the travel deals do not need to be repeatedly mentioned.
{{%expand "Provided Email Template"%}}
```
<!DOCTYPE html>
<html>
  <head>
    <title>Travel Tips Weekly Deals</title>
    <style>
      body {
        font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
        font-size: 16px;
        line-height: 1.5;
        color: #333;
        margin: 0;
        padding: 20px;
        background-color: #f5f5f5;
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: 100vh;
      }
      .content {
        background-color: #fff;
        border-radius: 10px;
        padding: 20px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        max-width: 600px;
        width: 100%;
        display: grid;
        grid-template-columns: 1fr;
      }
      .header {
        background-color: #3498db;
        padding: 20px;
        text-align: center;
        border-radius: 5px;
        margin-bottom: 20px;
        position: relative;
      }
      .header::after {
        content: "Exclusive Deals";
        display: block;
        position: absolute;
        bottom: 0;
        right: 0;
        background-color: #e74c3c;
        color: #fff;
        padding: 5px 10px;
        font-size: 12px;
        border-radius: 5px;
      }
      h1 {
        font-size: 24px;
        font-weight: bold;
        color: #fff;
        margin: 0;
        animation: 2s blink infinite;
      }
      p {
        margin-bottom: 10px;
      }
      ul {
        list-style: none;
        padding: 0;
        margin-bottom: 20px;
      }
      li {
        margin-bottom: 10px;
      }
      a {
        text-decoration: none;
        color: #fff;
        font-weight: bold;
        background-color: #3498db;
        display: inline-block;
        padding: 10px 20px;
        border-radius: 5px;
        transition: background-color 0.3s ease;
      }
      a:hover {
        background-color: #2c3e50;
      }
      @media only screen and (-webkit-min-device-pixel-ratio: 0) and (min-resolution: 0.001dpcm) {
        body {
          font-family: "Roboto", sans-serif;
        }
      }
      @keyframes blink {
        0% {
          opacity: 1;
        }
        50% {
          opacity: 0;
        }
        100% {
          opacity: 1;
        }
      }
    </style>
  </head>
  <body>
    <div class="content">
      <div class="header">
        <h1>Welcome to Travel Tips Weekly Deals!</h1>
      </div>
      <p>Check out these amazing travel deals from our partners:</p>
      <ul>
        <li>
          <a href="{{traveldeal1}}" ses:tags="partner:PartnerA"
            >Travel Deal 1</a
          >
        </li>
        <li>
          <a href="{{traveldeal2}}" ses:tags="partner:PartnerB"
            >Travel Deal 2</a
          >
        </li>
        <li>
          <a href="{{traveldeal3}}" ses:tags="partner:PartnerC"
            >Travel Deal 3</a
          >
        </li>
      </ul>
    </div>
  </body>
</html>
```
{{% /expand%}}

Add the email template to Amazon SES and try to send an email template to your mailbox, preferably one of them should be Gmail and another mailbox (Microsoft Exchange). You should see the results as below:

1. Good Rendering (e.g. Microsoft Exchange Mailbox)
<!-- image -->

2. Bad Rendering (e.g. Gmail on Browser)
<!-- image -->
{{% notice note %}}
There are free (and paid) email rendering preview tools on the market to help you test how your email would render depending on the client.
{{% /notice %}}


#### Steps:
1. Analyze the provided email template for the Weekly Deals campaign and identify the issue causing the rendering failure.
{{% notice tip %}}
Search for which css element Gmail does not support and remove the offending element so that the email renders uniformly across email clients. A good website to do so is https://www.caniemail.com/
{{% /notice %}}

2. Figure out how to dynamically populate the travel deals based on a passed array of travel deals data. Remember that you also need to retain the link tracking tags that we've configured in [Lab 7.1](../7.1-analyze-metrics)
{{% notice tip %}}
Take a look at the [advanced email personalization documentation](https://docs.aws.amazon.com/ses/latest/dg/send-personalized-email-advanced.html).
{{% /notice %}}

3. Update the email template back into Amazon SES.

4. Test the corrected email template and ensure that the rendering issue is resolved and the travel deals are populated dynamically based on the number of travel deals for the week. We have provided 2 commands below for your testing, you should receive an email with 3 travel deals using the first command, and another with 5 travel deals using the second command.
{{< tabs groupId="test-template" >}}
{{% tab name="3 Travel deals" %}}
**Command**
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
    "TemplateData": "{ \"travel_deals\": [ { \"name\": \"Travel Deal 1\", \"url\": \"https://examplepartnerA.com/deal1\", \"sestag\": \"partner:PartnerA\" }, { \"name\": \"Travel Deal 2\", \"url\": \"https://examplepartnerB.com/deal2\", \"sestag\": \"partner:PartnerB\" }, { \"name\": \"Travel Deal 3\", \"url\": \"https://examplepartnerC.com/deal3\", \"sestag\": \"partner:PartnerC\" } ] }"
  }
}'
```
**Expected Result**
<!-- image -->
{{% /tab %}}
{{% tab name="5 Travel deals" %}}
**Command**
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
    "TemplateData": "{ \"travel_deals\": [ { \"name\": \"Travel Deal 1\", \"url\": \"https://examplepartnerA.com/deal1\", \"sestag\": \"partner:PartnerA\" }, { \"name\": \"Travel Deal 2\", \"url\": \"https://examplepartnerB.com/deal2\", \"sestag\": \"partner:PartnerB\" }, { \"name\": \"Travel Deal 3\", \"url\": \"https://examplepartnerC.com/deal3\", \"sestag\": \"partner:PartnerC\" }, { \"name\": \"Travel Deal 4\", \"url\": \"https://examplepartnerD.com/deal4\", \"sestag\": \"partner:PartnerD\" }, { \"name\": \"Travel Deal 5\", \"url\": \"https://examplepartnerE.com/deal5\", \"sestag\": \"partner:PartnerE\" } ] }"
  }
}'

```
**Expected Result**
<!-- image -->
{{% /tab %}}
{{< /tabs >}}

### Optimize your email content
As a last step, do a final check to ensure the email content you sent out meet the following best-practices.

- Make sure your email has a subject and a body.
- Avoid sending overly short emails, especially if they contain images.
- Use full links instead of minified ones.
- Ensure all links in the email are working and redirect to a functional website. (For the purposes of this lab, we gave some example links above. Change them to another website that is acccessible.)
- Add a List-Unsubscribe header to improve your reputation, especially for promotional emails. (Refer to [Lab 5.4](../../5-ListAndSubscription/5.4-Subscription%20Management) for a recap.)
- Includes both HTML and plaintext parts to your email.

In this scenario, you've successfully diagnosed and fixed issues with the "Weekly Deals" email template. You identified the CSS elements causing rendering problems in Gmail and removed them to ensure uniform rendering across various email clients. Remember that it's alway best practice to test your email rendering on multiple email clients to make sure your email is accessible to your entire audience base. Additionally, you modified the template to dynamically populate the travel deals based on the provided data, making it more flexible and efficient. Lastly, you checked your email's content against best practice to ensure deliverability of your emails.

In the next scenario, you will focus on improving the deliverability of your emails. You will learn about various best practices, techniques, and configurations that will help increase the chances of your emails reaching the inbox of your subscribers.

