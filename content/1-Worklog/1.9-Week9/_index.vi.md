---
title: "Worklog Tuần 9"
date: "2025-09-09T19:53:52+07:00"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu Tuần 9

* Bắt đầu xây dựng nền tảng backend cho dự án Aurora Time.  
* Thiết lập hệ thống xác thực, bảng DynamoDB, API nền tảng và cơ chế nhắc lịch bằng EventBridge.  
* Hoàn thiện ước tính chi phí cho toàn bộ hạ tầng AWS được sử dụng.

---

### Công việc đã thực hiện trong tuần

| Ngày | Nội dung công việc | Bắt đầu | Hoàn thành | Tài liệu |
|------|---------------------|---------|------------|----------|
| **Thứ 2** | - Tạo Cognito User Pool và kiểm thử luồng đăng ký/đăng nhập qua Hosted UI.<br>- Kiểm tra cấu trúc ID/Access Token, hiểu các claims và cách API đọc danh tính người dùng. | 10/11/2025 | 10/11/2025 | Proposal – Cognito Authentication |
| **Thứ 3** | - Tạo bảng DynamoDB theo mô hình dữ liệu của Tuần 8 (Users, Events, Reminders).<br>- Thực hiện CRUD bằng Console và CLI.<br>- Kiểm tra thiết kế PK/SK và đánh giá nguy cơ hot partition. | 11/11/2025 | 11/11/2025 | Proposal – DynamoDB Data Model |
| **Thứ 4** | - Xây dựng POC API Gateway → Lambda → DynamoDB.<br>- Tạo 1–2 API đầu tiên (CreateEvent, ListEvents).<br>- Kiểm thử thành công luồng end-to-end. | 12/11/2025 | 12/11/2025 | Proposal – Serverless Architecture |
| **Thứ 5** | - Triển khai prototype nhắc lịch: EventBridge + Lambda + SES.<br>- Kiểm thử gửi email, xác minh domain/email trong SES và xem các giới hạn sandbox.<br>- Kiểm tra luồng kích hoạt nhắc lịch thành công. | 13/11/2025 | 13/11/2025 | Proposal – EventBridge & SES |
| **Thứ 6** | - Dùng AWS Pricing Calculator để ước tính chi phí hàng tháng cho các dịch vụ: Lambda, API Gateway, DynamoDB, Cognito, SES, EventBridge, S3, CloudFront, Amplify, CloudWatch.<br>- Ghi lại bảng chi phí dự kiến dựa trên mức sử dụng. | 14/11/2025 | 14/11/2025 | Proposal – Infrastructure Cost Estimate |

---

### Kết quả đạt được trong Tuần 9

* Thiết lập thành công hệ thống **xác thực người dùng** bằng Cognito User Pool.  
* Tạo và kiểm thử **bảng DynamoDB**, thực hiện CRUD và xác nhận mô hình dữ liệu hoạt động đúng.  
* Xây dựng các **API nền tảng** đầu tiên sử dụng API Gateway + Lambda + DynamoDB.  
* Hoàn thiện prototype **nhắc lịch tự động** bằng EventBridge + Lambda + SES.  
* Hoàn thành báo cáo **ước tính chi phí** cho toàn bộ dịch vụ AWS trong dự án Aurora Time.  
* Hiểu rõ hơn cách các dịch vụ serverless phối hợp với nhau trong một kiến trúc hoàn chỉnh.  
* Sẵn sàng bước sang Tuần 10 để mở rộng logic backend và tối ưu hệ thống.

---
