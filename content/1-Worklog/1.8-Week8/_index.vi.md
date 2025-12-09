---
title: "Week 8 Worklog"
date: "2025-09-09T19:53:52+07:00"
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives

* Hoàn thiện yêu cầu nghiệp vụ (business requirements) và user stories cho dự án **Aurora Time**.  
* Thiết kế kiến trúc serverless tổng thể cho ứng dụng (frontend + backend + database + automation).  
* Xây dựng mô hình dữ liệu DynamoDB và API contract cho backend.

---

### Tasks Completed This Week

| Day | Task | Start Date | Completion Date | Reference |
|-----|------|-------------|-----------------|-----------|
| **Mon** | - Hoàn thiện business requirements cho Aurora Time (quản lý lịch, nhắc lịch, đăng nhập, email thông báo).<br>- Xác định non-functional requirements: scalability, availability, latency, security, cost. | 03/11/2025 | 03/11/2025 | Proposal – Executive Summary & NFRs |
| **Tue** | - Thiết kế kiến trúc serverless: API Gateway, Lambda, DynamoDB, EventBridge Scheduler, SES, Cognito, Amplify Hosting, S3/CloudFront.<br>- Vẽ solution architecture diagram theo chuẩn AWS. | 04/11/2025 | 04/11/2025 | Proposal – Solution Architecture |
| **Wed** | - Thiết kế DynamoDB data model: bảng Users, Events, Reminders (PK/SK), các GSI cần thiết.<br>- Phân tích access patterns: list events theo ngày, get event details, update/delete, schedule lookup.<br>- Ước tính RCU/WCU theo workload. | 05/11/2025 | 05/11/2025 | Proposal – Technical Implementation Plan |
| **Thu** | - Xây dựng API contract cho backend: liệt kê các endpoint REST (GET/POST/PUT/DELETE).<br>- Định nghĩa request/response schema, error handling, validation rules.<br>- Mapping từng endpoint → Lambda function → IAM permissions cần thiết. | 06/11/2025 | 06/11/2025 | Proposal – API Design & IAM Roles |
| **Fri** | Tham dự sự kiện AWS để cập nhật kiến thức về serverless và event-driven architecture. | 07/11/2025 | 07/11/2025 | — |

---

### Week 8 Achievements

* Hoàn thiện **toàn bộ yêu cầu nghiệp vụ** cho dự án Aurora Time, bao gồm user stories và behaviour của từng chức năng.
* Xây dựng **kiến trúc serverless hoàn chỉnh** cho hệ thống, đảm bảo:  
  * không cần quản lý server  
  * tự động scale  
  * tối ưu chi phí  
  * phù hợp cho ứng dụng cá nhân và mở rộng được
* Thiết kế **mô hình DynamoDB chuẩn theo access pattern**, đảm bảo truy vấn nhanh và chi phí thấp.
* Xây dựng **API contract rõ ràng**, hỗ trợ phát triển frontend và backend song song.
* Hiểu rõ vai trò của các dịch vụ AWS trong kiến trúc ứng dụng:  
  * Cognito – Authentication  
  * API Gateway – Routing & API Management  
  * Lambda – Business Logic  
  * DynamoDB – NoSQL Database  
  * EventBridge – Scheduler & Automation  
  * SES – Email Notifications  
  * Amplify/S3/CloudFront – Frontend Hosting  
* Sẵn sàng bước sang giai đoạn tiếp theo: tạo skeleton code cho backend và xây dựng prototype UI.

---
