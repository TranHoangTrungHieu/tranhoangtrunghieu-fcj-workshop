---
title: " CRUD Sự kiện (Event Handler)"
date: 2025-12-09
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

{{% notice info %}}
📅 **Chức năng:** Hàm này xử lý toàn bộ thao tác Thêm (Create), Xem (Read), Sửa (Update), Xóa (Delete) đối với lịch trình của người dùng.
{{% /notice %}}

# Bước 1: Tạo Lambda Function
* **Tên hàm:** `auroraTimeEvent`
* **Runtime:** Node.js 18.x
* **Mô tả:** API xử lý CRUD cho bảng Events.

> **Hình ảnh:**
> ![Screenshot: Tạo hàm Aurora_EventHandler](images/lambda-event-create.png)

# Bước 2: Cấu hình IAM Role (Full Access to Events)
Chúng ta cần cấp toàn quyền cloudWatch trên bảng `events`.

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
                "arn:aws:logs:ap-southeast-1:080563425614:log-group:/aws/lambda/auroraTimeEvent:*"
            ]
        }
    ]
}
```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "AllowCRUDOnEventsTable",
			"Effect": "Allow",
			"Action": [
				"dynamodb:PutItem",
				"dynamodb:GetItem",
				"dynamodb:UpdateItem",
				"dynamodb:DeleteItem",
				"dynamodb:Query"
			],
			"Resource": "arn:aws:dynamodb:ap-southeast-1:080563425614:table/events"
		}
	]
}
```
## Bước 3: Code xử lý (Node.js) 
Quay trở lại giao diện Lambda Function, chúng ta sẽ viết code Node.js để xử lý các thao tác CRUD.
Sau khi hoàn thành, bấm **Deploy** để lưu lại.