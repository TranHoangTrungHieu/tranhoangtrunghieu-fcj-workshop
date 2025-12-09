---
title : "Giám sát & xử lý lỗi nhắc việc"
date : "2025-09-09T19:53:52+07:00"
weight : 4
chapter : false
pre : " <b> 5.4.4 </b> "
---

#### Tổng quan

Sau khi đã cấu hình EventBridge rule và Lambda gửi email nhắc việc, bước quan trọng tiếp theo là **giám sát** và **xử lý lỗi** để đảm bảo reminder luôn hoạt động ổn định.  
Phần này tập trung vào việc dùng **Amazon CloudWatch** và cấu hình retry/Dead-letter queue (DLQ) cho Lambda và EventBridge theo đúng định hướng “giảm rủi ro EventBridge/Lambda failure” trong proposal của Aurora Time.[web:254][web:297]

---

#### Theo dõi reminder bằng CloudWatch

1. Mở **CloudWatch console**, vào mục **Logs**:
   + Tìm log group của các hàm Lambda liên quan đến reminder, ví dụ:  
     - `/aws/lambda/AuroraTime-ScheduleReminder`  
     - `/aws/lambda/AuroraTime-SendReminderEmail`.
   + Mở log stream mới nhất để kiểm tra:
     - Số lượng reminder được xử lý.  
     - Các lỗi khi đọc DynamoDB hoặc khi gọi SES.[web:294]

2. Vào mục **Metrics**:
   + Chọn **Lambda** và theo dõi các metric:  
     - `Invocations`, `Errors`, `Duration`, `Throttles`.  
   + (Tuỳ chọn) Tạo **Alarm** khi:
     - `Errors` > 0 trong một khoảng thời gian liên tiếp.  
     - `Throttles` > 0, để bạn biết cần tăng concurrency hoặc tối ưu logic.

![CloudWatch metrics cho Lambda nhắc việc](/images/aurora-time/cloudwatch-metrics.png)

---

#### Cấu hình retry và Dead-letter queue

1. Với mỗi hàm Lambda reminder:

   + Trong phần **Asynchronous invocation**, cấu hình:
     - **Maximum retry attempts** (ví dụ 2–3 lần).  
     - **Dead-letter queue (DLQ)** trỏ tới một hàng **SQS** để lưu các event reminder bị lỗi nhiều lần.

2. Với **EventBridge rule/Scheduler**:

   + Bật **Retry policy** với backoff theo khuyến nghị (ví dụ: 2–5 lần retry, backoff 2x).  
   + (Tuỳ chọn) Cấu hình **Dead-letter queue** ở cấp EventBridge để ghi lại các event không gửi được tới Lambda.[web:254][web:297]

3. Tạo một Lambda hoặc script nhỏ đọc message từ DLQ để phân tích nguyên nhân lỗi (email invalid, user xoá event, cấu hình SES sai, v.v.) và cập nhật lại dữ liệu/bộ nhớ reminder nếu cần.

---

#### Kiểm thử kịch bản lỗi

1. Cố tình cấu hình sai một reminder (ví dụ email nhận không còn được verify hoặc DynamoDB thiếu trường bắt buộc) rồi để schedule chạy.

2. Kiểm tra:

   + CloudWatch Logs ghi lại lỗi tương ứng.  
   + Số lần retry của Lambda/EventBridge theo đúng cấu hình.  
   + Message lỗi xuất hiện trong DLQ nếu sau retry vẫn thất bại.

Bằng việc kết hợp CloudWatch, retry policy và DLQ, Aurora Time có thể phát hiện sớm sự cố trong pipeline nhắc việc và xử lý mà không làm gián đoạn toàn bộ hệ thống, đúng với phần **Risks & Mitigation** trong proposal của nhóm.
