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

[SESV2 API](https://docs.aws.amazon.com/ses/latest/APIReference-V2/) là thế hệ API kế tiếp phục vụ việc gửi và nhận emails. API này bao gồm rất nhiều tính năng mới bao gồm khả năng quản lý [danh sách người đăng kí](https://docs.aws.amazon.com/ses/latest/dg/sending-email-list-management.html) có sẵn ở SES, quản lý [các nhóm địa chỉ IP chuyên dụng](https://docs.aws.amazon.com/ses/latest/dg/dedicated-ip-pools.html), và khả năng tưởng tác với [Virtual Deliverability Manager](https://docs.aws.amazon.com/ses/latest/dg/vdm.html) qua API.

#### Tại sao việc nâng câos lên Amazon SES API v2 cần thiết

Việc nâng cấp mang đến rất nhiều lợi ích và đảm bảo rằng bạn có thể tận dụng các tính năng và bản vá mới nhất. Khi nâng cấp, bạn có thể:
1. **Tận dụng các chức năng mới**: Amazon SES API v2 cung cấp những tính năng và cải tiến mới trong đó tốt hơn trong khi cải thiện việc quản lý email. Khi lên phiên bản mới, bạn có thể tận dụng các tính năng này và tối ưu hoá quá trình email luân chuyển.

2. **Đảm bảo ứng dụng trong tương lai**: Bởi Amazon vẫn liên tục phát triển và giới thiệu những tính năng mới, những tính năng đó sẽ được phát hành tại bản Amazon SES API v2. Nâng cấp lên bản mới nhất đảm bảo rằng ứng dụng của bạn luôn luôn được cập nhật và tương thích với những bản cập nhật trong tương lai, tránh các vấn đề tương thích và gián đoạn tiềm ẩn.

3. **Nâng cao khả năng sử dụng và trải nghiệm của nhà phát triển**: Amazon SES API v2 được thiết kế thân thiện với người dùng và tương thích với các dịch vụ AWS khác. Với việc nâng cấp này, bạn có thể tiếp cận API trực quan hơn và xử lý lỗi tốt hơn, giúp cho việc phát triển, bảo trì và xử lý sự cố cho ứng dụng email của bạn.

Trong workshop này, chúng ta sẽ sử dụng v2 khi có thể, tận dụng các tính năng và chức năng bổ xung để điều hành các chiến lược email một cách hiệu quả.
