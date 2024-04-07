---
title : "Email and Domain Identities"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

### Creating and Verifying Email and Domain Identities
In this lab, we will explore the process of creating and verifying email and domain identities with Amazon Simple Email Service (SES). Properly managing email and domain identities is essential to maintain a good sender reputation and improve email deliverability.

#### Scenario
Your company, AWSomeNewsletter, is sending out a regular company newsletter via email. To improve your mailing reputation and ensure better email deliverability, you decide to set up a domain identity and verify it with Amazon SES. You will also verify an email identity to use as the sender address for your newsletter. In this workshop, we will guide you through setting up a domain identity, verifying an email identity, and configuring a custom MAIL FROM domain.

#### Email Identity and Domain Identity

{{< tabs groupId="email-domain-identity" >}}
{{% tab name="Email Identity" %}}

An email identity represents a specific email address. When you verify an email identity, you can use it as the sender address for your emails. However, this verification only applies to the exact email address you verified. Refer to the [email identity documentation](https://docs.aws.amazon.com/ses/latest/dg/creating-identities.html#verify-email-addresses-procedure) for more details.

{{% /tab %}}
{{% tab name="Domain Identity" %}}

A domain identity represents an entire domain. When you verify a domain identity, you can use any email address on that domain as the sender address for your emails. In addition, you can set up email authentication methods like DKIM and SPF for the domain, improving your mailing reputation and deliverability. Refer to the [domain identity documentation](https://docs.aws.amazon.com/ses/latest/dg/creating-identities.html#verify-domain-procedure) for more details.

{{% /tab %}}
{{< /tabs >}}

For a company newsletter, we recommend using a domain identity because it allows you to use any email address on your domain as the sender address, and it enables you to set up email authentication methods.
 
### Outline

The purpose of this lab is to guide you through the process of setting up your email and domain identities as well as enabling DomainKeys Identified Mail (DKIM) signing. This lab will have 2 parts:

1. **Creating and Verifying Email and Domain Identities**: We will discuss the differences between [email and domain identities](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-addresses-and-domains.html), and the benefits of using a domain identity for your company newsletter.
2. **Domain Identity - Verified Identities**: We will walk through the process of setting up a domain identity and obtaining the required verification information for your [DNS](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-domains.html).

### Content

1. [Email Identities](2.1-email-identity)
2. [Domain Identities](2.2-domain-identity)
