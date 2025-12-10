---
title: "Gửi Thông Báo (Send Reminder)"
date: 2025-12-09
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

{{% notice warning %}}
🔔 **Chức năng:** Hàm này được thiết kế để chạy định kỳ (ví dụ: mỗi 5 phút/lần bởi EventBridge Scheduler). Nó quét Database tìm các sự kiện sắp diễn ra trong vòng 15 phút tới và gửi email nhắc nhở qua API bên thứ 3.
{{% /notice %}}

# Bước 1: Tạo Lambda Function

Hàm này cần thời gian chạy lâu hơn bình thường một chút vì phải quét dữ liệu và chờ phản hồi từ API Mail, nên chúng ta sẽ tăng Timeout.

1.  **Tên hàm:** `sendReminder`
2.  **Runtime:** Node.js 24.x

> **Hình ảnh thực hiện:**
>
> ![Screenshot: Tạo hàm SendReminder ](/AWS/images/5-Workshop/lambdaSend.png)
> *Hình 5.4.3.1: Cấu hình hàm xử lý tác vụ nền (Background Job).*

---

# Bước 2: Cấu hình IAM Role (Full Access to Events)
**JSON Policy:**

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "logs:CreateLogGroup",
            "Resource": "arn:aws:logs:ap-southeast-1:080563425614:*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "logs:CreateLogStream",
                "logs:PutLogEvents"
            ],
            "Resource": [
                "arn:aws:logs:ap-southeast-1:080563425614:log-group:/aws/lambda/sendReminderLambda:*"
            ]
        }
    ]
}   ```
```
## Bước 3: Code xử lý (Node.js)
Quay trở lại giao diện Lambda Function, chúng ta sẽ viết code Node.js để quét dữ liệu sự kiện sắp diễn ra và gửi email nhắc nhở qua API bên thứ 3
> **Hình ảnh:**
> ![Screenshot: Tạo code](/AWS/images/5-Workshop/codeSend.png)
Sau khi hoàn thành, bấm **Deploy** để lưu lại.

```