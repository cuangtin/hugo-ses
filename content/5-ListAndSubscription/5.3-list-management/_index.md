---
title : "List Management"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---

In this workshop, you will learn how to set up list management for AWSomeNewsletter using Amazon Simple Email Service (SES) API v2. This will allow you to manage your mailing lists, create contact lists with various topics, and send emails to your subscribers.
{{% notice note %}}
This lab can only be done using the Amazon SES API and not in the Amazon SES console.
{{% /notice %}}

### Create a Contact List
Create a JSON file named `contact-list.json` with the following content. Customize the `Topics` array as needed for your AWSomeNewsletter:
```
{
  "ContactListName": "AWSomeNewsletterContactList",
  "Description": "Contact list for AWSomeNewsletter subscribers",
  "Topics": [
    {
      "TopicName": "TechNews",
      "DisplayName": "Latest Technology News",
      "Description": "Stay up-to-date with the latest technology trends, gadgets, and industry news.",
      "DefaultSubscriptionStatus": "OPT_IN"
    },
    {
      "TopicName": "HealthWellness",
      "DisplayName": "Health and Wellness Tips",
      "Description": "Get insights into maintaining a healthy lifestyle, nutrition advice, and mental wellness tips.",
      "DefaultSubscriptionStatus": "OPT_IN"
    },
    {
      "TopicName": "TravelTips",
      "DisplayName": "Smart Travel Tips",
      "Description": "Discover travel hacks, destination recommendations, and packing tips for your next adventure.",
      "DefaultSubscriptionStatus": "OPT_IN"
    },
    {
      "TopicName": "PersonalFinance",
      "DisplayName": "Money Management Tips",
      "Description": "Learn about budgeting, saving, investing, and making smart financial decisions.",
      "DefaultSubscriptionStatus": "OPT_IN"
    }
  ]
}
```

Run the following AWS CLI command to create the contact list:
```
aws sesv2 create-contact-list --cli-input-json file://contact-list.json
```
Add Contacts to the Contact List
{{< tabs groupId="contact-list" >}}
{{% tab name="Adding Contacts Individually" %}}
1. Create a JSON file named `contact.json` with the following content. Replace `example@amazon.com` with the email address of your first subscriber:
```
{
  "ContactListName": "AWSomeNewsletterContactList",

  "EmailAddress": "example@amazon.com",

  "UnsubscribeAll": false,

  "TopicPreferences": [
    {
      "TopicName": "TechNews",

      "SubscriptionStatus": "OPT_IN"
    }
  ],

  "AttributesData": "{\"firstName\": \"Jane\",\"lastName\": \"Doe\",\"city\": \"Singapore\",\"postalCode\": \"123456\"}"
}
```
In the example above, an `UnsubscribeAll` value of `false` shows that the contact has not unsubscribed from all topics, where a value of true would mean the contact has unsubscribed from all topics.

`TopicPreferences` includes information about the contact’s subscription status to topics. In the preceding example, the contact has opted in to the `TechNews` topic and will receive all emails to that topic.

The AttributesData is a JSON field where you can put any metadata about our contact. It must be a valid JSON object.

2. Run the following command:
```
aws sesv2 create-contact --cli-input-json file://contact.json
```
This command will add the contact specified in the `contact.json` file to the contact list mentioned in the file.
{{% /tab %}}
{{% tab name="Importing Contacts in Bulk" %}}
>Please note that there is a limitation when using Amazon SES sandbox: Bulk actions are disabled. As a result, the steps outlined in this lab will not work if your account is still operating within the Amazon SES sandbox. Please ensure your account is out of the sandbox before proceeding.

1. Create a new Amazon S3 bucket using the AWS CLI. Replace `your-bucket-name` with a unique name for your bucket:
```
aws s3api create-bucket --bucket your-bucket-name --region your-region
```

2. We can either use CSV or JSON format. Create a JSON file named `contacts.json` with the following content. Replace the email addresses with your subscribers' email addresses and update their topic preferences:
```
{
  "EmailAddress": "example1@amazon.com",
  "UnsubscribeAll": false,
  "AttributesData": "{\"firstName\": \"Jane\",\"lastName\": \"Doe\",\"city\": \"NYC\",\"postalCode\": \"111111\"}",
  "TopicPreferences": [
    {
      "TopicName": "TechNews",
      "SubscriptionStatus": "OPT_IN"
    },
    {
      "TopicName": "HealthWellness",
      "SubscriptionStatus": "OPT_OUT"
    },
    {
      "TopicName": "TravelTips",
      "SubscriptionStatus": "OPT_OUT"
    },
    {
      "TopicName": "PersonalFinance",
      "SubscriptionStatus": "OPT_OUT"
    }
  ]
}
{
  "EmailAddress": "example2@amazon.com",
  "UnsubscribeAll": true,
  "AttributesData": "{\"firstName\": \"John\",\"lastName\": \"Doe\",\"city\": \"Seattle\",\"postalCode\": \"123123\"}",
  "TopicPreferences": [
    {
      "TopicName": "TechNews",
      "SubscriptionStatus": "OPT_OUT"
    },
    {
      "TopicName": "HealthWellness",
      "SubscriptionStatus": "OPT_OUT"
    },
    {
      "TopicName": "TravelTips",
      "SubscriptionStatus": "OPT_IN"
    },
    {
      "TopicName": "PersonalFinance",
      "SubscriptionStatus": "OPT_IN"
    }
  ]
}
```
3. Upload the contacts file to the Amazon S3 bucket using the AWS CLI:
```
aws s3 cp contacts.json s3://your-bucket-name/contacts.json
```
Replace `your-bucket-name` with the name of your S3 bucket.

4. You need to create an Amazon SES identity policy that grants Amazon SES permission to read objects from your S3 bucket. Create a file named `ses-s3-policy.json` with the following content:
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ses.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```

5. Apply the policy to your S3 bucket:
```
aws s3api put-bucket-policy --bucket your-bucket-name --policy file://ses-s3-policy.json
```
Replace `your-bucket-name` with the name of your S3 bucket. 

6. Use the AWS CLI to start the import job:
```
aws sesv2 create-import-job --import-destination '{
  "ContactListDestination": {
    "ContactListName": "AWSomeNewsletter",
    "ContactListImportAction": "PUT"
  }
}' --import-data-source '{
  "S3Url": "s3://your-bucket-name/contacts.json",
  "DataFormat": "JSON"
}'
```
Replace `your-bucket-name` with the name of your bucket.

#### Verify Contacts in the Contact List
1. To verify that the contact has been added to the contact list, run:
```
aws sesv2 list-contacts --contact-list-name "AWSomeNewsletter" --page-size 10
```
You should see a list of contacts you have added in the previous steps in the JSON format, along with their Topic Subscription Preferences.

#### Removing Contacts from the Contact List
1. To remove a contact from the list, run:
```
aws sesv2 delete-contact --contact-list-name "AWSomeNewsletter" --email-address "ContactEmailAddress"
```
Similarly, you can also remove contact in bulk by specifying their email addressses in a JSON file. Instead of `"ContactListImportAction": "PUT"`, you would use `ContactListImportAction": "DELETE"`.

{{% /tab %}}
{{< /tabs >}}

In this lab, you learned how to set up list management for AWSomeNewsletter using Amazon Simple Email Service (SES) API v2. You learned how to create a contact list, add contacts to the list individually or in bulk, verify contacts in the contact list, and remove contacts from the list. By following these steps, you can easily manage your mailing lists, create contact lists with various topics, and send emails to your subscribers. With Amazon SES API v2, you can streamline your email marketing and communication efforts, reaching your audience with targeted messages that are relevant to their interests.