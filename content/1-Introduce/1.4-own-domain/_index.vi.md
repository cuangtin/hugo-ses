---
title : "Sử dụng domain của bạn"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 1.4 </b> "
---

### Những thuật ngữ quan trọng

- Tài khoản root: tài khoản AWS quản lý root domain (e.g. example.com) bên trong [vùng lưu trữ](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/hosted-zones-working-with.html). Bạn không nên làm việc trực tiếp domain này cho workshop vì bạn có thể vô tình làm hỏng các cấu hình DNS.
- Tài khoản service (IAM): tài khoản AWS mà bạn quản lý và xác thực tên miền của email (ví dụ sesworkshop.example.com)

Tên miền email của bạn sẽ là 1 sub-domain của root domain. Bạn có thể làm theo các bước sau để uỷ hosted zone root domain tới tài khoản service

### Tạo vùng lưu trữ
Điều này sẽ không được thực hiện tại tài khoản roor. Bạn sẽ tạp các sub-domain trong tài khoản service

{{% notice note %}}
Hosted zone phải thuộc **public hosted zone**.
{{% /notice %}}

ZoneName phải là tiền tố của root domain của bạn, Giả sử root domain của bạn là `example.com`, ZoneName sẽ dạng như là `sesworkshop.example.com`.

### Tạo DNS records cho root account 

Đầu tiên, truy cập **root account**, sau đó chuyển hướng đến bảng điều khiển Route53, chọn hosted zone mà bạn đã đăng kí trên Route53, lưu lại zone id - dạng `Z02271753ICPZ8MJC84MI`
![Zone Id](/hugo-ses/images/1/4/0001.png?featherlight=false&width=70pc)

Tiếp đó, truy cập **service account**, truy cập bảng điều khiển Route53, chọn hosted zone vừa tạo:
![DNS records](/hugo-ses/images/1/4/0002.png?featherlight=false&width=70pc)

Copy nội dung của trường "Value" của NS record. Trở lại root account, thêm 1 NS record vào tập hợp DNS. giá trị là name servers từ *service account hosted zone**.

Sau khi hoàn thành, hosted zone sẽ có NS record như sau:
![DNS records](/hugo-ses/images/1/4/0003.png?featherlight=false&width=70pc)

### Kiểm tra DNS records đã hoạt động hay chưa
Đợi 5-10 phút, kiểm tra bằng cách: 

Truy cập terminal và chạy `host -a sesworkshop.example.com`.

Đầu ra sẽ có dạng: 

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

{{%expand "Đầu ra khi không thành công" %}}
```
Received 136 bytes from 127.0.0.1#53 in 8 ms
Trying "sesworkshop.example.com.iad7.corp.amazon.com"
Trying "sesworkshop.example.com.iad7.amazon.com"
Trying "sesworkshop.example.com.amazon.com"
Host psesworkshop.example.com. not found: 3(NXDOMAIN)
```
{{% /expand%}}

### Bài lab liên quan:

- [2.2: Domain Identities](../../2-create-domain/2.2-domain-identity)
- [7.3: Optimize Your "Weekly Deals" and "Daily Updates" emails for Deliverability](../../7-capstone-project/7.3-deliverability)

