---
title : "SES and SESv2 API"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 1.2 </b> "
---

## Key Differences and the Benefits of Migrating

Amazon Simple Email Service (SES) is a cloud-based email sending service that helps businesses and developers send marketing, notification, and transactional emails. Amazon has been continuously improving its services, and as a result, the Amazon SES API v2 was introduced. In this workshop, we'll be primarily focusing on the newer Amazon SES API v2. In this section, we'll discuss the differences between Amazon SES and Amazon SES API v2 and the benefits of migrating to the newer version.

#### AWS SES API

[The AWS SES API](https://docs.aws.amazon.com/ses/latest/APIReference/) is the original API provided by AWS for sending and receiving emails. It is a relatively simple API that provides basic functionality for sending and receiving emails. The API has been around for several years and is well established in the market.

#### SESV2 API

[The SESV2 API](https://docs.aws.amazon.com/ses/latest/APIReference-V2/) is the next generation API for sending and receiving emails. The API includes several new features, including the ability to manage [lists and subscriptions](https://docs.aws.amazon.com/ses/latest/dg/sending-email-list-management.html) natively within SES, manage [dedicated IP Pools](https://docs.aws.amazon.com/ses/latest/dg/dedicated-ip-pools.html), and the ability to interact with the [Virtual Deliverability Manager](https://docs.aws.amazon.com/ses/latest/dg/vdm.html) through the API.

#### Why Migrating to Amazon SES API v2 is Necessary

Migrating to Amazon SES API v2 offers several benefits and ensures that you can take advantage of the latest features and improvements. By migrating, you can:


1. **Leverage New Features**: Amazon SES API v2 includes new features and enhancements that provide better functionality and improved email management. By moving to the newer version, you can take advantage of these improvements and optimize your email sending process.
2. **Future-proof Your Application**: As Amazon continues to develop and introduce new features, they will be released in the Amazon SES API v2. Migrating to the newer version ensures that your application stays up-to-date and compatible with future updates, avoiding potential compatibility issues and disruptions.
3. **Improve Usability and Developer Experience**: Amazon SES API v2 is designed to be more user-friendly and consistent with other AWS services. By migrating, you can benefit from a more intuitive API and better error handling, making it easier to develop, maintain, and troubleshoot your email sending application.

In this workshop, we will be using SESv2 wherever possible, leveraging its additional features and functionality to manage our email campaigns more effectively.
