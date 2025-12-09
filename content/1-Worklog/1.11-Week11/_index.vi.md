---
title: "Worklog Tuần 11"
date: "2025-09-09T19:53:52+07:00"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11

* Triển khai các thành phần backend cốt lõi cho Aurora Time (Cognito, DynamoDB, Lambda, API Gateway).  
* Xây dựng một Proof of Concept (POC) hoàn chỉnh cho chức năng đăng nhập và quản lý sự kiện.  
* Thiết lập workflow gửi email nhắc lịch bằng EventBridge + SES.  
* Ước tính chi phí vận hành của toàn bộ hệ thống.

---

### Công việc đã thực hiện trong tuần

| Ngày | Nhiệm vụ | Bắt đầu | Hoàn thành | Tài liệu |
|------|----------|----------|------------|----------|
| **Thứ 2** | - Tạo Cognito User Pool và cấu hình luồng đăng ký / đăng nhập.<br>- Kiểm tra authentication bằng Hosted UI và phân tích ID/Access token.<br>- Ghi lại cách backend sẽ đọc claims từ token để phân quyền. | 24/11/2025 | 24/11/2025 | Proposal – Cognito & Authentication |
| **Thứ 3** | - Tạo các bảng DynamoDB ban đầu (Users, Events, Reminders).<br>- Kiểm tra CRUD bằng Console và AWS CLI.<br>- Xác minh thiết kế partition key và ghi nhận các nguy cơ hot-partition. | 25/11/2025 | 25/11/2025 | Proposal – DynamoDB Data Model |
| **Thứ 4** | - Xây dựng backend POC: API Gateway + Lambda (CreateEvent, GetEvents).<br>- Kết nối Lambda với DynamoDB bằng IAM role tối thiểu quyền.<br>- Kiểm thử luồng đầy đủ: HTTP → API Gateway → Lambda → DynamoDB. | 26/11/2025 | 26/11/2025 | Proposal – Serverless Architecture |
| **Thứ 5** | - Cấu hình EventBridge + Lambda + SES để gửi email nhắc lịch the
