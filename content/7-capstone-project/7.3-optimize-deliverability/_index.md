---
title : "Optimize Deliverability"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 7.3 </b> "
---

## Optimize Your "Weekly Deals" and "Daily Updates" emails for Deliverability

In this scenario, we will guide you on how to optimize your email deliverability using Amazon SES and some best practices to achieve high deliverability rates. By following these steps, you can increase the likelihood that your emails will reach your recipients' inboxes and avoid being marked as spam. You've optimized your [content rendering](https://catalog.us-east-1.prod.workshops.aws/workshops/e4a4aa26-fb17-45eb-9edf-77b7f8b6035f/en-US/lab-6/lab-6-2/) and [set up tracking](https://catalog.us-east-1.prod.workshops.aws/workshops/e4a4aa26-fb17-45eb-9edf-77b7f8b6035f/en-US/lab-6/lab-6-1/) for each configuration sets. The last piece of the puzzle for deliverability is to manage your **reputation** with the Email Service Providers (ESPs).

If you've been following along with the previous lab and sending emails from Amazon SES, there is a very high chance that your emails would have ended up in the Spam inbox like below.
<!-- image -->
{{% notice note %}}
In the worst case scenario, your email/domain identities might be blocked by the ESPs, preventing you from reaching your audience altogether. Once you're in this state, it becomes extremely hard to recover. Therefore, we recommend setting up your email environment CORRECTLY before starting to send out mass emails.
{{% /notice %}}

### Scenario
In preparation for the upcoming campaign for the `Weekly Deals` and `Daily Updates`, you've been tasked by the `Health & Wellness` and `Travel Tips` Business Units to make sure that the emails will be deliverable.

**Task**: Optimize your email deliverability by managing your email environment's reputation and configure SES to follow best practices.

**Steps**:

Let's establish a baseline on how "spammy" your email is. Send a test email to the **mail-tester** address to get a result.

1. Let's establish a baseline on how "spammy" your email is. Send a test email to the mail-tester address to get a result.
{{% notice tip %}}
Consider using a tool like [mail-tester](https://www.mail-tester.com/) to evaluate the deliverability of your emails. Send a test email to the provided address and receive an analysis of your email's likelihood to be delivered to the inbox.
{{% /notice %}}

Your result, assuming you are sending from your own verified email address using the template in [Lab 3.4](../../3-SendEmail/3.4-testmail-aws-cli) should be similar to below:
<!-- image [Email Score Before] -->
If you drill down into the result you'd see that the majority of point deductions will come from setting up your domain incorrectly. This is what we will address in the next part.

2. [OPTIONAL] Set up a custom domain for sending emails.

    a. If you don't already have a domain, purchase one from AWS Route 53 or another provider.

    b. Create a new domain identity in AWS SES using the purchased domain.
{{% notice tip %}}
If you haven't set up your own domain, refer to [Lab 2.2](../../2-create-domain/2.2-domain-identity/) on how to do so.
{{% /notice %}}

    c. Configure a custom MAIL FROM domain by choosing a subdomain of your domain, such as notifications.example.com.

    d. If your domain is hosted on Route 53, enable automatic DNS updates for the MAIL FROM domain.

{{% notice tip %}}
Check this [documentation] to learn how to configure your custom MAIL FROM domain.
{{% /notice %}}

3. Add a DMARC (Domain-based Message Authentication, Reporting, and Conformance) record to your domain's DNS.

    a. Create a _dmarc TXT record with the value `v=DMARC1; p=none`.

    b. This record indicates that you've set up DMARC and allows recipients to reject emails with authentication failures.

After completing these steps, you can expect improved email deliverability and a lower likelihood of your emails being marked as spam. Remember that maintaining high-quality email content and following best practices are crucial for ensuring your emails reach your users' inboxes. Send a test email again using your newly configured DOMAIN, your SES environment is now ready to send out emails!
<!-- image -->

4. [OPTIONAL] You can also follow this [blog post](https://aws.amazon.com/blogs/messaging-and-targeting/what-is-bimi-and-how-to-use-it-with-amazon-ses/) to set up Brand Indicators for Message Identification or BIMI to allow your email recipient to display a brand's logo next to the brand's authenticated message.
This will help your recipients recognize your brand logo on the email and improve open rates.