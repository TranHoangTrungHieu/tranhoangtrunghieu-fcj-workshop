---
title : "Backend Aurora Time"
date : "2025-09-09T19:53:52+07:00"
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Sử dụng API Gateway, Lambda và DynamoDB

Trong phần này, bạn sẽ xây dựng lớp **backend serverless** cho Aurora Time bằng cách kết hợp **Amazon API Gateway**, **AWS Lambda** và **Amazon DynamoDB**. Backend này chịu trách nhiệm xử lý toàn bộ nghiệp vụ CRUD cho sự kiện (events), lịch (schedules) và nhắc việc (reminders), sau đó cung cấp API cho frontend gọi thông qua HTTP.[web:111][web:282]

Các hàm Lambda sẽ nhận request từ API Gateway, ghi/đọc dữ liệu trong bảng DynamoDB và trả về response theo định dạng JSON thống nhất. Việc sử dụng kiến trúc serverless giúp hệ thống tự động mở rộng, không cần quản lý server và chi phí chỉ phát sinh khi có request truy cập.

![Tổng quan backend Aurora Time](/images/aurora-time/backend-overview.png)

#### Nội dung

- [Thiết kế & tạo bảng DynamoDB](5.3.1-dynamodb/)
- [Triển khai Lambda functions & API Gateway](5.3.2-lambda-apigw/)
