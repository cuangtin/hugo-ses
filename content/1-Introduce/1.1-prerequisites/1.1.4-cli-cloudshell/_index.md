---
title : "CLI and AWS CloudShell"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 1.1.4 </b> "
---

## AWS CLI

If you haven't already, install the AWS CLI on your local machine. You can follow the installation instructions provided in the official AWS documentation:
- [Installing the AWS CLI version 2](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) 
> For me, I run the workshop under Ubuntu 20.04, so that I follow the **Linux x86 (64-bit)** instruction:
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

Check if success, run command `aws --version`:
```
aws-cli/1.27.83 Python/3.8.2 Linux/5.15.146.1-microsoft-standard-WSL2 awscrt/0.16.10 botocore/1.29.83
```

After installing the AWS CLI, configure it with your AWS credentials by running the following command: `` aws configure ``
```
ubuntu@ip-address:~$ aws configure
AWS Access Key ID []: AKIA4XXXXXXXX
AWS Secret Access Key []: FJieXXXXXXXXXXXXXXXX
Default region name []: ap-south-1
Default output format []:
```

## AWS Cloudshell

You can also use [AWS CloudShell](https://aws.amazon.com/cloudshell/) to run the commands from the Web Browser.

Using AWS CloudShell, a browser-based shell, you can quickly run scripts with the AWS Command Line Interface (CLI), experiment with service APIs using the AWS CLI, and use other tools to increase your productivity. The CloudShell icon appears in AWS Regions where CloudShell is available.

#### Uploading Files with CloudShell

In the labs, you will sometimes have to upload a file to CloudShell to access it in the terminal (e.g. an email template file in HTML). To do so, click on the `` Actions `` button on the top right corner of the CloudShell and then click on `` Upload file ``.

![Access](/hugo-ses/images/1/4/cloudshell.png?featherlight=false&width=70pc)