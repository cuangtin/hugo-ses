---
title : "Tài khoản AWS và IAM User"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 1.1.2 </b> "
---

In order to interact with AWS services, you need an AWS account. Furthermore, you need an IAM user for this account that you can use to log into the AWS Management Console, so that you can provision and configure you resources.

[AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/) enables you to manage access to AWS services and resources securely. Using IAM, you can create and manage AWS users and groups, and use permissions to allow and deny their access to AWS resources.

#### Bringing your own AWS account

The regular case is that you have to bring your own AWS account, configured with an IAM user with administrator privileges. If possible, this should be a sandbox account away from any company production resources (if applicable).

If you don't have an AWS account yet, and you want to repeat this workshop for yourself later, you can create a free account [here](https://portal.aws.amazon.com/billing/signup).

#### Create IAM User

Now proceed to creating an IAM user to login with for the purposes of this workshop.

1. Once you have an AWS account, create a new IAM user for this workshop with access to the AWS account: [Create a new IAM user to use for the workshop](https://console.aws.amazon.com/iam/home?#/users$new)

2. Enter the user details and select Access Type as AWS Management Console Access. 
<!-- image -->
3. Attach the following managed policies from Attach Existing Policies directly:

    AWSCloudFormationFullAccess, AmazonSESFullAccess, AmazonSNSFullAccess, AmazonDynamoDBFullAccess, CloudWatchFullAccess, IAMFullAccess

    Click Next → Ignore Tags → Next Review

4. Click Create user to create the new user.

5. Now you can log into the [AWS Console](https://aws.amazon.com/console/) with the user you have created with IAM.