---
title : "Capstone Project Solutions"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 7.5 </b> "
---

### Scenario 1: Analyzing Metrics for "Weekly Deals" and "Daily Updates" Campaigns'
#### Health and Wellness Business Unit Configuration
1. Configure the Health & Wellness Configuration Set to track open rates using CloudWatch.
```
aws sesv2 create-configuration-set-event-destination \
--configuration-set-name HealthWellnessConfigSet \
--event-destination-name OpensPerCampaign \
--event-destination '{
    "Enabled": true,
    "MatchingEventTypes": ["OPEN"],
    "CloudWatchDestination": {
        "DimensionConfigurations": [
            {
                "DimensionName": "campaign",
                "DimensionValueSource": "MESSAGE_TAG",
                "DefaultDimensionValue": "January"
            }
        ]
    }
}'
```

2. Sending Weekly Deals emails test
a. January Campaign
```
aws sesv2 send-email \
    --from-email-address sender@example.com \
    --destination ToAddresses=recipient@example.com\
    --content '{"Simple": {"Subject": {"Data": "Test Email","Charset": "UTF-8"},"Body": {"Text": {"Data": "This is a test email sent using the AWS CLI SESv2.","Charset": "UTF-8"},"Html": {"Data": "This is a test email sent using the AWS CLI SESv2.","Charset": "UTF-8"}}}}' \
    --configuration-set HealthWellnessConfigSet \
    --email-tags Name=campaign,Value=January
```
b. February Campaign
```
aws sesv2 send-email \
    --from-email-address sender@example.com \
    --destination ToAddresses=recipient@example.com\
    --content '{"Simple": {"Subject": {"Data": "Test Email","Charset": "UTF-8"},"Body": {"Text": {"Data": "This is a test email sent using the AWS CLI SESv2.","Charset": "UTF-8"},"Html": {"Data": "This is a test email sent using the AWS CLI SESv2.","Charset": "UTF-8"}}}}' \
    --configuration-set HealthWellnessConfigSet \
    --email-tags Name=campaign,Value=February
```

#### Travel Business Unit Configuration
1. Modify the HTML template such that each link is tagged with its corresponding partner name. We assume the file name is `travel_tips_weekly_deals.html`
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
        <a href="{{traveldeal1}}" ses:tags="partner:PartnerA">Travel Deal 1</a>
      </li>

      <li>
        <a href="{{traveldeal2}}" ses:tags="partner:PartnerB">Travel Deal 2</a>
      </li>

      <li>
        <a href="{{traveldeal3}}" ses:tags="partner:PartnerC">Travel Deal 3</a>
      </li>
    </ul>
  </body>
</html>
```
```
aws sesv2 create-email-template --cli-input-json "$(printf '{"TemplateName": "TravelTipsWeeklyDeals", "TemplateContent": {"Subject": "Travel Tips Weekly Deals", "Html": "%s"}}' "$(sed -e ':a' \
-e 'N' \
-e '$!ba' \
-e 's/\n/\\n/g' \
-e 's/"/\\"/g' \
travel_tips_weekly_deals.html)")"
```

3. Configure the Travel Tips Configuration Set to track click rates using CloudWatch.
```
aws sesv2 create-configuration-set-event-destination \
--configuration-set-name TravelTipsConfigSet \
--event-destination-name PartnerClick \
--event-destination '{
    "Enabled": true,
    "MatchingEventTypes": ["CLICK"],
    "CloudWatchDestination": {
        "DimensionConfigurations": [
            {
                "DimensionName": "partner",
                "DimensionValueSource": "LINK_TAG",
                "DefaultDimensionValue": "-"
            }
        ]
    }
}'
```

4. Set up a dashboard in Cloudwatch to track Click Through to each affiliate partner links
```
aws cloudwatch put-dashboard --dashboard-name TravelAgencyTracking --dashboard-body '{
    "widgets": [
        {
            "type": "metric",
            "x": 0,
            "y": 0,
            "width": 24,
            "height": 6,
            "properties": {
                "metrics": [
                    ["AWS/SES", "Click", "partner", "PartnerA", {"label": "Partner A", "stat": "Sum"}],
                    ["AWS/SES", "Click", "partner", "PartnerB", {"label": "Partner B", "stat": "Sum"}],
                    ["AWS/SES", "Click", "partner", "PartnerC", {"label": "Partner C", "stat": "Sum"}]
                ],
                "view": "singleValue",
                "region": "<your-region>",
                "title": "Partner Metrics",
                "period": 86400
            }
        }
    ]
}'
```

### Scenario 2: Diagnosing and Fixing Issues with the "Weekly Deals" Email Template

1. Analyze the provided email template for the Weekly Deals campaign and identify the issue causing the rendering failure.
    #### Issues you should identify
- The position: absolute; and `position: relative;` properties in the `.header` and `.header::after` selectors might not work properly, causing the **Exclusive Deals** label to be misplaced or not displayed at all.
- The `@keyframes` animation for the `blink` effect on the h1 element may not work in Gmail, so the blinking effect might not be displayed.
- The `@media` query for detecting pixel ratios may not be properly supported, and the `font-family` change might not be applied.
2. Figure out how to dynamically populate the travel deals based on a passed array of travel deals data.
The final template, with invalid html/css tags removed and passing array logic is found below:
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
    </style>
  </head>
  <body>
    <div class="content">
      <div class="header">
        <h1>Welcome to Travel Tips Weekly Deals!</h1>
      </div>
      <p>Check out these amazing travel deals from our partners:</p>
      <ul>
        {{#each travel_deals}}
        <li>
          <a href="{{url}}" ses:tags="{{sestag}}">{{name}}</a>
        </li>
        {{/each}}
      </ul>
    </div>
  </body>
</html>
```

### Scenario 4: Building and Segmenting Your Lists for sending "Weekly Deals" Campaigns
#### Python Lambda Function Solution
```
import json
import boto3

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('EngagementTable')

def lambda_handler(event, context):
    for record in event['Records']:
        sns_message = json.loads(record['body'])
        ses_event = json.loads(sns_message['Message'])

        if ses_event["eventType"] in ("Open", "Click"):
            email_address = ses_event["mail"]["destination"][0]
            timestamp = ses_event["mail"]["timestamp"]

            update_engagement(email_address, timestamp)

def update_engagement(email, timestamp):
    table.update_item(
        Key={
            'email': email
        },
        UpdateExpression='SET last_engagement_date = :val1',
        ExpressionAttributeValues={
            ':val1': timestamp
        }
    )
```

#### Node.js Lambda Function Solution
```
const AWS = require("aws-sdk");
const dynamodb = new AWS.DynamoDB.DocumentClient();
const tableName = "EngagementTable";

exports.handler = async (event) => {
  for (const record of event.Records) {
    const snsMessage = JSON.parse(record.body);
    const sesEvent = JSON.parse(snsMessage.Message);

    if (["Open", "Click"].includes(sesEvent.eventType)) {
      const emailAddress = sesEvent.mail.destination[0];
      const timestamp = sesEvent.mail.timestamp;

      await updateEngagement(emailAddress, timestamp);
    }
  }
};

async function updateEngagement(email, timestamp) {
  const params = {
    TableName: tableName,
    Key: {
      email: email,
    },
    UpdateExpression: "SET last_engagement_date = :val1",
    ExpressionAttributeValues: {
      ":val1": timestamp,
    },
  };

  await dynamodb.update(params).promise();
}
```
