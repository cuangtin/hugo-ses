---
title : "Using Your Own Domain"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 1.4 </b> "
---

### Important Terminologies
- Root Account: the AWS account where you have hosted your root domain (e.g. example.com) in a [hosted zone](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/hosted-zones-working-with.html). You should not be working straight out of your root account for this workshop as you might inadvertently compromise your DNS configurations.
- Service Account: the AWS account where you will be hosting and verifying your email domain (e.g. sesworkshop.example.com) to be used for this workshop.

For this workshop, your email domain will be a sub-domain of your root domain. You can follow the steps below to delegate your root domain hosted zone to the service account.

### Create the hosted zones in your service accounts
This will NOT happen in the root account. You will be creating the sub-domains in the service account.

{{% notice note %}}
These hosted zones MUST be **PUBLIC Hosted Zones**.
{{% /notice %}}

The zoneName must be suffixed with whatever you purchased as your root domain. Assuming your root domain is ` example.com ` the hosted zone name will be something like ` sesworkshop.example.com `.

### Create DNS records in the root account
First, go into your **root account**, and then to the Route53 console, and click on the hosted zone that you registered your domain in Route53 with, and get the hosted zone id. It should be a string like: ` Z02271753ICPZ8MJC84MI `

Second, go into your **service account**, and go to the route53 console, and click on the hosted zone that you just created. It should look something like this:

Look at the NS record, and copy the contents of the "Value" field. Now, go back to the root account, and add a NS record for DNS delegation. The value should be the name servers from the **service account hosted zone**.

Once done, your hosted zone in your **root account** should have the NS record like this:

### Check to see if the DNS records resolve
Wait 5-10 minutes after the DNS entries deploy to your root account hosted zone in order to do this check.

Go to your terminal and run ` host -a sesworkshop.example.com `.

The output should look something like:

```
Trying "sesworkshop.example.com"
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 21563
;; flags: qr rd ra; QUERY: 1, ANSWER: 5, AUTHORITY: 0, ADDITIONAL: 8

;; QUESTION SECTION:
;sesworkshop.example.com. IN ANY

;; ANSWER SECTION:
sesworkshop.example.com. 172800 IN NS ns-1394.awsdns-46.org.
sesworkshop.example.com. 172800 IN NS ns-1800.awsdns-33.co.uk.
sesworkshop.example.com. 172800 IN NS ns-844.awsdns-41.net.
sesworkshop.example.com. 172800 IN NS ns-115.awsdns-14.com.
sesworkshop.example.com. 900 IN SOA ns-115.awsdns-14.com. awsdns-hostmaster.amazon.com. 1 7200 900 1209600 86400

;; ADDITIONAL SECTION:
ns-115.awsdns-14.com. 40015 IN A 205.251.192.115
ns-115.awsdns-14.com. 39155 IN AAAA 2600:9000:5300:7300::1
ns-1394.awsdns-46.org. 38793 IN A 205.251.197.114
ns-1394.awsdns-46.org. 38455 IN AAAA 2600:9000:5305:7200::1
ns-1800.awsdns-33.co.uk. 38743 IN A 205.251.199.8
ns-1800.awsdns-33.co.uk. 38969 IN AAAA 2600:9000:5307:800::1
ns-844.awsdns-41.net. 38591 IN A 205.251.195.76
ns-844.awsdns-41.net. 38574 IN AAAA 2600:9000:5303:4c00::1

Received 428 bytes from 192.168.0.1#53 in 2420 ms
```

As a correctness check, here is what you should see if the DNS records do NOT resolve correctly:

{{%expand "Unsuccessful Resolve Output" %}}
```
Received 136 bytes from 127.0.0.1#53 in 8 ms
Trying "sesworkshop.example.com.iad7.corp.amazon.com"
Trying "sesworkshop.example.com.iad7.amazon.com"
Trying "sesworkshop.example.com.amazon.com"
Host psesworkshop.example.com. not found: 3(NXDOMAIN)
```
{{% /expand%}}

### Relevant Labs
The following labs will require a custom domain:

- [2.2: Domain Identities](../../2-create-domain/2.2-domain-identity)
- [7.3: Optimize Your "Weekly Deals" and "Daily Updates" emails for Deliverability](../../7-capstone-project/7.3-deliverability)

