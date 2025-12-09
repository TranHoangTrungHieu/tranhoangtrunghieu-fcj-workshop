---
title : "Chuẩn bị tài nguyên cho nhắc việc"
date : "2025-09-09T19:53:52+07:00"
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---

Để chuẩn bị cho phần này của workshop, bạn sẽ cấu hình các dịch vụ cần thiết để Aurora Time có thể gửi email nhắc việc (reminder) một cách serverless, bao gồm:

+ Kích hoạt và cấu hình **Amazon SES** trong đúng region của Aurora Time.
+ Xác minh (verify) địa chỉ email gửi và, nếu còn ở sandbox, cả địa chỉ nhận.
+ Tạo **IAM role** cho Lambda được phép gửi email qua SES và được **Amazon EventBridge** gọi theo lịch.[web:259][web:289]

Các thành phần này làm việc cùng nhau để cho phép Aurora Time gửi email nhắc việc đúng thời điểm mà không cần bất kỳ máy chủ riêng nào.

---

#### Kích hoạt và xác minh Amazon SES

1. Mở **Amazon SES console** tại region bạn triển khai Aurora Time (ví dụ: `ap-southeast-1` hoặc `us-east-1`).

2. Trong thanh điều hướng, chọn **Verified identities**, sau đó click **Create identity**.

![SES identities](/images/aurora-time/ses-identities.png)

3. Trong màn hình **Create identity**:

   + **Identity type**: chọn **Email address**.  
   + **Email address**: nhập địa chỉ email sẽ dùng làm địa chỉ gửi nhắc việc, ví dụ: `aurora-time-notify@your-domain.com`.  
   + Giữ nguyên các thiết lập mặc định khác, sau đó click **Create identity**.

4. Mở hộp thư của bạn, click vào đường dẫn xác minh mà SES gửi tới.  
   Khi trạng thái identity trong SES chuyển sang **Verified**, Lambda mới có thể gửi email thành công.[web:294]

---

#### Tạo IAM role cho Lambda gửi email

1. Mở **IAM console**, chọn **Roles** → **Create role**.

2. Ở phần **Trusted entity type**, chọn **AWS service**.  
   Trong **Use case**, chọn **Lambda**, rồi click **Next** để tiếp tục.

3. Gắn các permission sau:

   + Managed policy **AWSLambdaBasicExecutionRole** để Lambda ghi log lên CloudWatch.  
   + Một inline policy tuỳ chỉnh cho phép gửi email qua SES, ví dụ:

{
"Version": "2012-10-17",
"Statement": [
{
"Sid": "AllowSendEmail",
"Effect": "Allow",
"Action": [
"ses:SendEmail",
"ses:SendRawEmail"
],
"Resource": "*"
}
]
}

4. Đặt tên role, ví dụ **AuroraTimeReminderLambdaRole**, kiểm tra lại các quyền rồi click **Create role**.

![IAM role cho Lambda nhắc việc](/images/aurora-time/iam-reminder-role.png)

Role này sẽ được sử dụng cho các Lambda **ScheduleReminder** và **SendReminderEmail** ở các bước tiếp theo.

---

#### Chuẩn bị EventBridge cho nhắc việc

1. Mở **Amazon EventBridge console** trong cùng region.

2. Ở thanh điều hướng bên trái, chọn **Scheduler** (hoặc **Rules**, tuỳ cách bạn triển khai reminder).

![Chuẩn bị EventBridge](/images/aurora-time/eventbridge-prepare.png)

3. Đảm bảo bạn có thể:

   + Tạo **rule** hoặc **schedule** mới.  
   + Chọn **target** là Lambda (sau này sẽ là hàm gửi nhắc việc).  
   + Cấu hình cron/fixed schedule cho các thử nghiệm reminder.[web:254][web:257]

---

Đến đây, bạn đã:

+ Kích hoạt và verify địa chỉ email trong SES.  
+ Tạo IAM role cho Lambda với quyền gửi email.  
+ Chuẩn bị EventBridge để tạo rule/scheduler.

Trong phần **5.4.2**, bạn sẽ tạo rule/scheduler cụ thể trên EventBridge và viết Lambda để gửi email nhắc việc cho các sự kiện của Aurora Time.
