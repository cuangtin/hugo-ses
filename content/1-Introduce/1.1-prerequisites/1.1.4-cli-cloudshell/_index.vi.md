---
title : "CLI và AWS CloudShell"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 1.1.4 </b> "
---

## AWS CLI

Làm theo hướng dẫn cài đặt từ trang chủ của AWS: [cài đặt AWS CLI phiên bản 2](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) 
> Mình sử dụng trên máy chủ Ubuntu 20.04 nên dùng hướng dẫn của **Linux x86 (64-bit)**:
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

Kiểm tra sau khi cài đặt, nhập `aws --version`:
```
aws-cli/1.27.83 Python/3.8.2 Linux/5.15.146.1-microsoft-standard-WSL2 awscrt/0.16.10 botocore/1.29.83
```

Sau khi cài đặt, thiết lập thông tin xác thực bằng cách chạy: `` aws configure ``
```
ubuntu@ip-address:~$ aws configure
AWS Access Key ID []: AKIA4XXXXXXXX
AWS Secret Access Key []: FJieXXXXXXXXXXXXXXXX
Default region name []: ap-south-1
Default output format []:
```

## AWS Cloudshell

Bạn cũng có thể sử dụng [AWS CloudShell](https://aws.amazon.com/cloudshell/) để chạy các lệnh từ trình duyệt.

AWS CloudShell - 1 trình môi trường dòng lệnh trên trình duyệt - giúp bạn thực thi lệnh sử dụng AWS CLI. Dịch vụ này chỉ được support ở các AWS Regions cụ thể.

#### Tải lên file với CloudShell

Trong workshop này, bạn sẽ phải tải lên các file để CloudShell truy cập và chạy command (ví dụ như mẫu email dạng HTML). Theo hướng dẫn sau:

![Access](/hugo-ses/images/1/4/cloudshell.png?featherlight=false&width=70pc)