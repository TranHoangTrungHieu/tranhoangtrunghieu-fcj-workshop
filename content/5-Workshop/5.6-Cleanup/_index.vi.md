---
title : "Dọn dẹp tài nguyên"
date : "2025-09-09T19:53:52+07:00"
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

#### Dọn dẹp tài nguyên

Xin chúc mừng bạn đã hoàn thành xong workshop Aurora Time!  
Trong workshop này, bạn đã triển khai một ứng dụng quản lý thời gian cá nhân dựa trên kiến trúc **serverless** của AWS: API Gateway, Lambda, DynamoDB, EventBridge, SES, Cognito, Amplify, S3/CloudFront. Bạn cũng đã cấu hình nhắc việc tự động qua email và ước lượng chi phí hạ tầng hàng tháng.[web:111]

Để tránh phát sinh chi phí sau khi hoàn thành lab, hãy dọn dẹp toàn bộ tài nguyên đã tạo.[web:324][web:327]

---

#### Dọn dẹp

1. **Xoá frontend Aurora Time (Amplify, S3, CloudFront)**  

   + Mở **AWS Amplify console**, chọn ứng dụng Aurora Time → **App settings** → **Delete app**, xác nhận xoá.
   + Mở **S3 console**, chọn bucket chứa static files frontend (nếu còn):  
     - Chọn **Empty** để xoá toàn bộ object, sau đó **Delete** bucket.
   + Nếu bạn tạo riêng một **CloudFront distribution** cho frontend:
     - Disable distribution, chờ trạng thái `Disabled`, sau đó chọn **Delete**.

   ![Xoá ứng dụng Amplify](/images/aurora-time/cleanup-amplify.png)

2. **Xoá backend API (API Gateway & Lambda)**  

   + Vào **API Gateway console**, chọn REST API Aurora Time → **Delete** API.
   + Vào **Lambda console**, lần lượt chọn và xoá các hàm Lambda dùng trong workshop (CreateEvent, ListEvents, UpdateEvent, DeleteEvent, ScheduleReminder, SendReminderEmail, …).

   ![Xoá API Gateway và Lambda](/images/aurora-time/cleanup-backend.png)

3. **Xoá bảng DynamoDB**  

   + Mở **DynamoDB console**, chọn bảng `AuroraTimeEvents` (và các bảng khác nếu có, ví dụ `AuroraTimeReminders`).  
   + Chọn **Delete table**, gõ lại tên bảng để xác nhận.

   ![Xoá bảng DynamoDB](/images/aurora-time/cleanup-dynamodb.png)

4. **Xoá EventBridge rules/Schedules và SES identities**

   + Trong **EventBridge console**, xoá rule/schedule dùng cho reminder (ví dụ `AuroraTime-ReminderSchedule`).  
   + Trong **SES console**, nếu chỉ dùng địa chỉ email cho lab, có thể xoá **Verified identity** tương ứng để tránh nhầm lẫn về sau.

   ![Xoá rule EventBridge](/images/aurora-time/cleanup-eventbridge.png)

5. **Xoá Cognito User Pool và dọn CloudWatch Logs**  

   + Mở **Cognito console**, xoá **User Pool** Aurora Time (kèm users và groups test).  
   + Mở **CloudWatch console**, vào **Log groups**, tìm các log group của Lambda Aurora Time và xoá nếu không còn cần tham chiếu.

   ![Xoá Cognito & log](/images/aurora-time/cleanup-cognito-logs.png)

6. **Xoá IAM roles/policies dùng riêng cho workshop (tuỳ chọn)**  

   + Trong **IAM console**, xoá các role/policy chỉ phục vụ Aurora Time, ví dụ:  
     - `AuroraTimeReminderLambdaRole`  
     - Role cho API/Lambda được bạn tạo riêng.
   + Đảm bảo các role này không còn được gắn cho service nào khác trước khi xoá.

   ![Xoá IAM role](/images/aurora-time/cleanup-iam.png)


