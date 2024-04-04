---
title : "Creating email templates"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 6.1 </b> "
---

In this lab, we will explore how to create email templates using Amazon SES. Email templates can save time and help ensure consistency in branding and messaging across multiple emails. We will create an HTML email template relevant to the AWSomeNewsletter use case, without including any variables in the template for now.

{{% notice note %}}
This lab can only be done using the Amazon SES API and not in the Amazon SES console.
{{% /notice %}}

#### Step 1: Create the HTML email template
Create a new file named "awesome_newsletter_template.html" and add the following HTML code to create a basic email template for AWSomeNewsletter:
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
      <p>Hello AWSomeNewsletter subscriber!</p>
      <p>
        Here's a roundup of the latest news and articles in your chosen interest
        area:
      </p>
      <ul>
        <li><a href="#">Article 1: Exciting News in Your Interest Area</a></li>
        <li><a href="#">Article 2: Developments You Should Know About</a></li>
        <li><a href="#">Article 3: What Experts Are Saying</a></li>
      </ul>
      <p>Stay tuned for more updates next month!</p>
      <p class="footer">
        If you no longer wish to receive these emails, please
        <a href="#">unsubscribe</a>.
      </p>
    </div>
  </body>
</html>
```
Preview your HTML using your favorite browser or code editors. It should look similar to the following:
![Template](/hugo-ses/images/6/1/0001.png?featherlight=false&width=50pc)

#### Step 2: Create the email template using the AWS CLI
Now, we will create a new email template in Amazon SES using the AWS CLI.
{{% notice note %}}
If you're using the AWS Cloudshell, you'd need to first upload the awesome_newsletter_template.html file to AWS Cloudshell before proceeding.
{{% /notice %}}
Run the following command to create the email template in Amazon SES:
```
aws sesv2 create-email-template --cli-input-json "$(printf '{"TemplateName": "AWSomeNewsletterTemplate", "TemplateContent": {"Subject": "AWSomeNewsletter Monthly Digest", "Html": "%s"}}' "$(sed -e ':a' \
-e 'N' \
-e '$!ba' \
-e 's/\r\n/\\n/g' \
-e 's/\n/\\n/g' \
-e 's/"/\\"/g' \
awesome_newsletter_template.html)")"
```
This command reads the content of the `awesome_newsletter_template.html` file, removes newline characters, and escapes double quotes. Then, it creates the email template with the modified HTML content using the AWS CLI. Note that we've also specified a template name of `AWSomeNewsletterTemplate` and a template subject `AWSomeNewsletter Monthly Digest` in the same command.

Now you have successfully created an email template using Amazon SES and AWS CLI. In the next section, we will learn how to personalize this template with dynamic content.

To view the created email template using the AWS CLI, run the following command:
```
aws sesv2 get-email-template --template-name AWSomeNewsletterTemplate
```

If you were successful in the previous step, this command will return the email template details, including the HTML and text parts of the template.

Remember to refer to the [Amazon SES Developer Guide](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/send-personalized-email-api.html) for more information on working with email templates and the AWS CLI.

In the next part of this lab [Lab 6.2](../6.2-personalizing), we will introduce dynamic content to the email template and learn how to personalize it for different customer segments.