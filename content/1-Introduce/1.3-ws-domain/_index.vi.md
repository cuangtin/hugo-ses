---
title : "Sử dụng domain mặc định của workshop"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 1.3 </b> "
---

#### Những thuật ngữ quan trọng

Tên miền email của bạn sẽ là 1 sub-domain của domain gốc của workshop (ví dụ sesworkshop.online), kiểu {thứ tự team}.sesworkshop.online (1.sesworkshop.online hoặc 2.sesworkshop.online). Bạn có thể làm theo các bước dưới đây để xác thực domain và xác nhận domain hoạt động chính xác. Trong phần còn lại của workshop, hãy thay thế example.,com với domain của bạn.

#### Kiểm tra việc xác thực domain

Sử dụng AWS CLI, bạn có thể kiểm tra trạng thái của domain bằng cách chạy câu lệnh sau:

```
aws sesv2 get-email-identity --email-identity {{Your domain name}}
```

Bạn sẽ nhận được 1 phản hồi dạng JSON trong đó giá trị `VerifiedForSendingStatus` là `true`.

Dưới đây là 1 phản hồi mẫu:

```
{
    "IdentityType": "DOMAIN",
    "FeedbackForwardingStatus": true,
    "VerifiedForSendingStatus": true,
    "DkimAttributes": {
        "SigningEnabled": true,
        "Status": "SUCCESS",
        "Tokens": [
            "oc4vbmhlp2jdgulaqmj64h4a5ea6rvhi",
            "cw3h654y4ufvu7ux4a2mf2bec3le3sw4",
            "67cc7cuhbidfnrxmaocfq33jtdyutqfi"
        ],
        "SigningAttributesOrigin": "AWS_SES",
        "NextSigningKeyLength": "RSA_2048_BIT",
        "CurrentSigningKeyLength": "RSA_2048_BIT",
        "LastKeyGenerationTimestamp": "2024-03-28T23:15:43.083000+07:00"
    },
    "MailFromAttributes": {
        "BehaviorOnMxFailure": "USE_DEFAULT_VALUE"
    },
    "Policies": {},
    "Tags": [],
    "ConfigurationSetName": "my-first-configuration-set",
    "VerificationStatus": "SUCCESS",
    "VerificationInfo": {
        "LastCheckedTimestamp": "2024-03-28T23:26:44.115000+07:00",
        "LastSuccessTimestamp": "2024-03-28T23:26:44.441000+07:00",
        "ErrorType": "HOST_NOT_FOUND",
        "SOARecord": {
            "PrimaryNameServer": "amalia.ns.cloudflare.com",
            "AdminEmail": "dns.cloudflare.com",
            "SerialNumber": 1
        }
    }
}
```

Ngoài ra, bạn có thể truy cập [bảng điều khiển của Amazon SES](https://us-east-1.console.aws.amazon.com/ses/), chọn `Identities` bên trong thanh bên trái và xác nhận danh tính domain có status là `Verified`

![Identity](/hugo-ses/images/1/3/identity.png?featherlight=false&width=70pc)