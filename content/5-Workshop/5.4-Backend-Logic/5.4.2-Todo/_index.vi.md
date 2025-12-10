---
title: "CRUD Todo (Công việc)"
date: 2025-12-09
weight: 1
chapter: false
pre: " <b> 5.4.2. </b> "
---

{{% notice info %}}
📅 **Chức năng:** Hàm này xử lý toàn bộ thao tác Thêm (Create), Xem (Read), Sửa (Update), Xóa (Delete) đối với lịch trình của người dùng.
{{% /notice %}}

# Bước 1: Tạo Lambda Function
* **Tên hàm:** `auroratimeTodo`
* **Runtime:** Node.js 24.x
* **Mô tả:** API xử lý CRUD cho bảng todo.

> **Hình ảnh:**
> ![Screenshot: Tạo hàm Aurora_TodoHandler](/AWS/images/5-Workshop/lambdaTodo.png)

# Bước 2: Cấu hình IAM Role (Full Access to Events)
Chúng ta cần cấp toàn quyền cloudWatch trên bảng `todo`.

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
                "logs:PutLogTodo"
            ],
            "Resource": [
                "arn:aws:logs:ap-southeast-1:080563425614:log-group:/aws/lambda/auroraTimeTodo:*"
            ]
        }
    ]
}
```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "AllowCRUDOnTodoTable",
			"Effect": "Allow",
			"Action": [
				"dynamodb:PutItem",
				"dynamodb:GetItem",
				"dynamodb:UpdateItem",
				"dynamodb:DeleteItem",
				"dynamodb:Query"
			],
			"Resource": "arn:aws:dynamodb:ap-southeast-1:080563425614:table/todo"
		}
	]
}
```
## Bước 3: Code xử lý (Node.js)
Quay trở lại giao diện Lambda Function, chúng ta sẽ viết code Node.js để xử lý các thao tác CRUD.
> **Hình ảnh:**
> ![Screenshot: Tạo code](/AWS/images/5-Workshop/codeTodo.png)
Sau khi hoàn thành, bấm **Deploy** để lưu lại.