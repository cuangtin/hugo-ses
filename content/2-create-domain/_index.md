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

{{< tabs groupId="config" >}}
{{% tab name="json" %}}
```json
{
  "Hello": "World"
}
```
{{% /tab %}}
{{% tab name="XML" %}}
```xml
<Hello>World</Hello>
```
{{% /tab %}}
{{% tab name="properties" %}}
```properties
Hello = World
```
{{% /tab %}}
{{< /tabs >}}
