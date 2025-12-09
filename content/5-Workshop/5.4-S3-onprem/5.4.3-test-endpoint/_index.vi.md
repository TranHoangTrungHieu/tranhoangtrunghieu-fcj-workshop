---
title : "Kiểm tra luồng nhắc việc (Reminder Flow)"
date : "2025-09-09T19:53:52+07:00"
weight : 3
chapter : false
pre : " <b> 5.4.3 </b> "
---

#### Tạo sự kiện có nhắc việc trong Aurora Time

1. Mở giao diện web **Aurora Time** (đã được deploy qua AWS Amplify) và đăng nhập bằng tài khoản Cognito của bạn.

2. Ở màn hình lịch (day/week/month), chọn nút **Tạo sự kiện mới**.

3. Điền thông tin sự kiện:
   + Tiêu đề: ví dụ `Demo reminder`.
   + Thời gian bắt đầu/kết thúc: chọn thời điểm trong vòng 5–10 phút tới để dễ kiểm tra.
   + Tuỳ chọn **Reminder**: chọn “Nhắc trước 5 phút” (hoặc giá trị tương đương mà backend đang hỗ trợ).

![Tạo sự kiện có nhắc việc](/images/aurora-time/frontend-create-event.png)

4. Nhấn **Lưu** và kiểm tra lại trên giao diện lịch để xác nhận sự kiện đã được tạo thành công.

---

#### Xác nhận dữ liệu trong DynamoDB

1. Mở **DynamoDB console**, chọn bảng `AuroraTimeEvents`.

2. Dùng **Explore table items** (hoặc query theo `userId`) để tìm item vừa tạo:
   + Trường `userId` khớp với user hiện tại (lấy từ Cognito).
   + Trường `eventKey` hoặc các thuộc tính `startTime`, `reminderOffset` chứa đúng thông tin bạn đã nhập.

![Kiểm tra item trong DynamoDB](/images/aurora-time/dynamodb-events.png)

3. Đảm bảo rằng trường dùng cho reminder (ví dụ `reminderAt` hoặc `reminderOffset`) đã được lưu; đây là dữ liệu mà Lambda sẽ dùng để quyết định gửi email.

---

#### Kiểm tra EventBridge và Lambda xử lý reminder

1. Mở **Amazon EventBridge console**, chọn schedule/rule `AuroraTime-ReminderSchedule` đã tạo ở bước 5.4.2 và xác nhận trạng thái đang là **Enabled**.

![Rule EventBridge đã tạo](/images/aurora-time/eventbridge-rule-created.png)

2. Mở **CloudWatch Logs**, tìm log group của Lambda xử lý reminder (ví dụ `/aws/lambda/AuroraTime-ScheduleReminder`).

3. Sau khi tới gần thời điểm reminder:
   + Reload log stream mới nhất và kiểm tra nội dung log:  
     - Lambda tìm thấy event/reminder của bạn.  
     - Lambda gọi hàm gửi email (trực tiếp hoặc thông qua một Lambda khác như `SendReminderEmail`).[web:259][web:289]

![Log Lambda xử lý reminder](/images/aurora-time/cloudwatch-metrics.png)

---

#### Xác nhận email nhắc việc đã được gửi

1. Mở hộp thư tương ứng với địa chỉ email bạn đã dùng đăng ký/đăng nhập (hoặc email được cấu hình làm recipient trong SES).

2. Sau khi schedule chạy, bạn sẽ nhận được một email từ địa chỉ đã verify trong SES (ví dụ `aurora-time-notify@your-domain.com`) với nội dung nhắc lại tiêu đề, thời gian và ghi chú của sự kiện.

![Email nhắc việc từ Aurora Time](/images/aurora-time/reminder-email.png)

3. Nếu không thấy email:
   + Kiểm tra thư mục Spam/Quảng cáo.  
   + Xem lại CloudWatch Logs của Lambda gửi email và bảng SES (Sending statistics, EventBridge integration) để tìm lỗi cấu hình quyền hoặc địa chỉ nhận chưa được verify khi còn ở sandbox.[web:294]

Sau khi hoàn thành các bước trên, bạn đã kiểm tra end‑to‑end luồng nhắc việc của Aurora Time: từ việc người dùng tạo sự kiện, lưu vào DynamoDB, EventBridge kích hoạt Lambda, cho đến SES gửi email reminder đến hộp thư người dùng.
