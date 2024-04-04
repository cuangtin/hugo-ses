---
title : "Tài khoản AWS và IAM User"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 1.1.2 </b> "
---

Để có thể sử dụng các dịch vụ trong AWS, bạn cần 1 tài khoản AWS. Ngoài ra, bạn cũng cần một tài khoản IAM thuộc tài khoản AWS này cho phép bạn cung cấp và cấu hình quyền sử dụng tài nguyên của bạn.

[AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/) cho phép bạn quản lý quyền truy cập và các dịch vụ và tài nguyên của AWS 1 cách an toàn.

#### Thiết lập tài khoản AWS cho riêng mình

Trường hợp phổ biến là bạn thiết lập 1 tài khoản người dùng IAM với quyền quản trị viên. Nếu được, đây nên là tài khoản sandbox, tách biệt hoàn toàn với tài nguyên hệ thống đang vận hành của công ty hiện tại.

Nếu bạn chưa có tài khoản AWS, hãy đăng kí miên phí [tại đây](https://portal.aws.amazon.com/billing/signup).

#### Tạo tài khoản người dùng IAM

Tiến hành tạo tài khoản IAM phục vụ nhu cầu của workshop:
1. Khi đã có tài khoản AWS, tạo 1 tài khoản IAM có quyền truy cập vào tài khoản AWS: [Tạo tài khoản IAM](https://console.aws.amazon.com/iam/home?#/users$new)
    ![Create IAM User](/hugo-ses/images/1/2/navigate.png?featherlight=false&width=70pc)
    ![Create IAM User](/hugo-ses/images/1/2/create.png?featherlight=false&width=70pc)

2. Nhập thông tin của người dùng chọn chọn Access Type as AWS Management Console Access.
    ![Fill in Credentials](/hugo-ses/images/1/2/account-info.png?featherlight=false&width=70pc)

3. Đính kèm các chính sách sau qua Attach Policies directly:
    AWSCloudFormationFullAccess, AmazonSESFullAccess, AmazonSNSFullAccess, AmazonDynamoDBFullAccess, CloudWatchFullAccess, IAMFullAccess
    ![Attach Policies](/hugo-ses/images/1/2/attack-policies.png?featherlight=false&width=70pc)

4. Click Create user.
    ![Reviews](/hugo-ses/images/1/2/reviews.png?featherlight=false&width=70pc)
    ![Store Credentials](/hugo-ses/images/1/2/store-access.png?featherlight=false&width=70pc)

5. Giờ bạn có thể đăng nhập vào [bảng điều khiển](https://aws.amazon.com/console/) với tài khoản IAM bạn vừa tạo.