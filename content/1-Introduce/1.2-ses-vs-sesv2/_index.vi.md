---
title : "SES và SESv2 API"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 1.2 </b> "
---

## Những điểm khác biệt và lợi ích khi nâng cấp

Amazon Simple Email Service (SES) là 1 dịch vụ gửi mail dựa trên đám mây giúp các doanh nghiệp và lập trình viến gửi những email giao dịch, email thông báo cũng như email tiếp thị. Amazon đã và đang hoàn thiện hơn các dịch vụ của họ, và kết quả là Amazon SES API v2 ra đời. Trong workshop này, chúng ta sẽ hầu như tập trung vào API v2. Chúng ta sẽ thảo luận 1 chút về điểm khác biệt giữa AWS SES API và AWS SES API v2 và lợi ích của việc nâng cấp lên phiên bản mới.

#### AWS SES API

[The AWS SES API](https://docs.aws.amazon.com/ses/latest/APIReference/) là API gốc được cung cấp bởi AWS. Đây là mẫu API tương đối đơn giản cung cấp các chức năng cơ bản cho việc gửi và nhận email. Phiên bản này đã ra mắt được nhiều năm và có chỗ đứng vững chắc trên thị trường.

#### AWS SESV2 API

[The SESV2 API](https://docs.aws.amazon.com/ses/latest/APIReference-V2/) is the next generation API for sending and receiving emails. The API includes several new features, including the ability to manage [lists and subscriptions](https://docs.aws.amazon.com/ses/latest/dg/sending-email-list-management.html) natively within SES, manage [dedicated IP Pools](https://docs.aws.amazon.com/ses/latest/dg/dedicated-ip-pools.html), and the ability to interact with the [Virtual Deliverability Manager](https://docs.aws.amazon.com/ses/latest/dg/vdm.html) through the API.

#### Why Migrating to Amazon SES API v2 is Necessary

Migrating to Amazon SES API v2 offers several benefits and ensures that you can take advantage of the latest features and improvements. By migrating, you can:


1. **Leverage New Features**: Amazon SES API v2 includes new features and enhancements that provide better functionality and improved email management. By moving to the newer version, you can take advantage of these improvements and optimize your email sending process.
2. **Future-proof Your Application**: As Amazon continues to develop and introduce new features, they will be released in the Amazon SES API v2. Migrating to the newer version ensures that your application stays up-to-date and compatible with future updates, avoiding potential compatibility issues and disruptions.
3. **Improve Usability and Developer Experience**: Amazon SES API v2 is designed to be more user-friendly and consistent with other AWS services. By migrating, you can benefit from a more intuitive API and better error handling, making it easier to develop, maintain, and troubleshoot your email sending application.

In this workshop, we will be using SESv2 wherever possible, leveraging its additional features and functionality to manage our email campaigns more effectively.
