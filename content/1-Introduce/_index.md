---
title : "Introduction"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

## Introduction to Amazon Simple Email Service

In this hands-on workshop, you will learn how to effectively manage email sending, subscriptions, and deliverability for the AWSomeNewsletter company using Amazon Simple Email Service (SES). By the end of this workshop, you will have a comprehensive understanding of email management best practices and the tools available in Amazon SES.

#### Target Audience

This workshop is designed for developers, email and IT infrastructure administrators who want to learn how to set up, manage and optimize their email sending environment with Amazon Simple Email Service.

#### Expected Outcomes

Upon completing this comprehensive workshop, you will gain in-depth knowledge and hands-on experience with Amazon SES. You will understand how to effectively set up and configure an Amazon SES environment, manage contact lists and subscriptions, and work efficiently with email templates. Additionally, you will become proficient in improving email deliverability rates and enhancing sender reputation. You will also be well-equipped to apply these email management concepts and best practices to real-world scenarios, ensuring that your organization's email infrastructure runs optimally.

#### Duration

The workshop is designed to be completed in 6-7 hours.

#### Prerequisites

This workshop assumes you have a basic understanding of AWS services and their related terminologies. Prior experience with Amazon Web Services (AWS) Command Line Interface (CLI) and knowledge of Simple Mail Transfer Protocol (SMTP) and email protocols will be advantageous. Additionally, familiarity with the basics of email management, including concepts such as suppression lists and sender reputation, would be beneficial. While the workshop is designed to be comprehensive and beginner-friendly, having a basic background in these areas will enable you to make the most out of this learning experience.

#### Cost considerations

While the workshop itself is free of charge, please note that performing the labs may incur charges on your AWS account as you will be leveraging various AWS resources. Amazon SES, like many AWS services, follows a pay-as-you-go pricing model, so you will only pay for what you use. For cost-saving, ensure that you clean up your resources after performing the experiments or when they're no longer in use. Please refer to the official AWS Pricing page for Amazon SES to gain a clear understanding of the potential costs. Always be mindful of your usage and remember that you're responsible for any charges incurred in your AWS account during this workshop.

Most of the Amazon Web Services used in this workshop are eligible for Free Tier (always free, 12-months free, or free trials). You can get more details on AWS Free Tier page about each service. Some services are not eligible for Free Tier:

- Kinesis Data Streams
- Kinesis Data Firehose

Detailed calculation for Athena, Kinesis Data Streams and Kinesis Data Firehose is available [here](https://calculator.aws/#/estimate?id=2023cba18cb2dc3517ca2159bb744abde87c1546) . You can use it as a reference and adjust to your needs (e.g. different region, or usage).

If you are not eligible for Free tier, or to estimate the cost of your solution architecture, which you are going to build with these services after the workshop, you can use [AWS Pricing Calculator](https://calculator.aws/#/) and pricing pages for each service.

#### Workshop Scenario

AWSomeNewsletter is a rapidly growing company that sends various types of newsletters to their subscribers. They need an efficient way to manage their mailing lists, track user subscriptions, create and manage email templates, and ensure high deliverability rates and a good sender reputation.

In this workshop, you will explore different Amazon SES features and tools that will help AWSomeNewsletter to effectively manage their email infrastructure.

#### Clean resources

Once you're done with the workshop, please ensure to follow the clean up steps listed [here](../6-cleanup/).

## Contents

- [Prerequisites](1.1-prerequisites/)
- [A note on SES versus SESv2 API](1.2-ses-vs-sesv2/)
- [Using the default workshop domain](1.3-ws-domain/)
- [Using Your Own Domain](1.4-own-domain/)

Get ready to dive into the world of email management with Amazon SES and help AWSomeNewsletter achieve their email marketing goals!
