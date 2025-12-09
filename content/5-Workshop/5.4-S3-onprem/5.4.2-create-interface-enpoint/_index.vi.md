---
title : "Tạo luật EventBridge cho nhắc việc"
date : "2025-09-09T19:53:52+07:00"
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

Trong phần này, bạn sẽ tạo và kiểm thử **EventBridge rule/Scheduler** để kích hoạt Lambda gửi email nhắc việc cho người dùng Aurora Time.  
Luật này sẽ chạy theo lịch (ví dụ vài phút một lần) và gọi hàm Lambda đọc các reminder sắp đến trong DynamoDB, sau đó gửi email qua SES.[web:254][web:289]

1. Mở **Amazon EventBridge console** trong region đã dùng cho Aurora Time.

2. Trong thanh điều hướng bên trái:
   + Nếu bạn dùng **Scheduler**: chọn **Scheduler** → click **Create schedule**.  
   + Nếu bạn dùng **Rules**: chọn **Rules** → click **Create rule**.

![Chuẩn bị tạo rule EventBridge](/images/aurora-time/eventbridge-prepare.png)

3. Ở phần cấu hình cơ bản:

   + **Name**: `AuroraTime-ReminderSchedule`  
   + **Description**: Lập lịch kích hoạt Lambda gửi email nhắc việc cho Aurora Time.  
   + **Schedule pattern**:  
     - Chọn **Recurring schedule**.  
     - Ví dụ chọn `Rate` = **5 minutes** để trong môi trường lab, reminder được chạy thường xuyên cho dễ quan sát.

![Cấu hình lịch chạy](/images/aurora-time/eventbridge-schedule.png)

4. Ở phần **Target**:

   + **Target type**: chọn **AWS service**.  
   + **Target**: **Lambda function**.  
   + **Function**: chọn hàm Lambda dùng để xử lý reminder, ví dụ: `AuroraTime-ScheduleReminder`.  
   + **Execution role**: chọn IAM role đã tạo ở bước 5.4.1 (ví dụ `AuroraTimeReminderLambdaRole`), role này phải có quyền `lambda:InvokeFunction` (nếu dùng Scheduler) và quyền gửi email qua SES trong chính Lambda.[web:259][web:297]

![Chọn Lambda target](/images/aurora-time/eventbridge-rule.png)

5. (Tuỳ chọn) Ở phần **Input**, bạn có thể:

   + Để **Constant (JSON text)** rỗng nếu Lambda tự tính thời gian reminder cần xử lý.  
   + Hoặc truyền một payload đơn giản, ví dụ:
{
"source": "eventbridge-scheduler",
"task": "process-upcoming-reminders"
}

6. Kiểm tra lại toàn bộ cấu hình rồi click **Create schedule** (hoặc **Create rule** nếu dùng Rules).  
Sau khi tạo xong, trạng thái schedule/rule sẽ là **Enabled** và bắt đầu gọi Lambda theo chu kỳ định sẵn.

![Rule EventBridge đã được tạo](/images/aurora-time/eventbridge-rule-created.png)

Chúc mừng bạn đã tạo thành công luật EventBridge cho Aurora Time. Ở bước tiếp theo, bạn sẽ kiểm thử luồng nhắc việc end‑to‑end: tạo event có reminder, chờ schedule chạy và xác nhận email được gửi đến hộp thư người dùng.
