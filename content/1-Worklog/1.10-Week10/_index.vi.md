---
title: "Week 10 Worklog"
date: "2025-09-09T19:53:52+07:00"
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives

* Hoàn thiện các yêu cầu nghiệp vụ (business requirements) cho Aurora Time.  
* Xây dựng kiến trúc serverless ở mức high-level và hoàn chỉnh mô hình dữ liệu DynamoDB.  
* Thiết kế nền tảng bảo mật và cơ chế xác thực cho hệ thống.

---

### Tasks Completed This Week

| Day | Task | Start Date | Completion Date | Reference |
|-----|-------|-------------|-----------------|-----------|
| **Mon** | - Rà soát và hoàn thiện yêu cầu nghiệp vụ & user stories cho Aurora Time (lịch biểu, nhắc lịch, xác thực, email).<br>- Xác định yêu cầu phi chức năng: độ trễ, độ sẵn sàng, mở rộng, tối ưu chi phí. | 17/11/2025 | 17/11/2025 | Proposal – Executive Summary, Problem Statement |
| **Tue** | - Thiết kế kiến trúc serverless tổng thể: API Gateway, Lambda, DynamoDB, EventBridge, SES, Cognito, Amplify, S3/CloudFront.<br>- Cập nhật sơ đồ kiến trúc (architecture diagram) theo bản proposal. | 18/11/2025 | 18/11/2025 | Proposal – Solution Architecture |
| **Wed** | - Hoàn thiện mô hình dữ liệu DynamoDB: thiết kế bảng, PK/SK cho Users, Events, Schedules, Reminders.<br>- Ghi tài liệu access patterns: tạo/sửa/xóa events, truy vấn theo ngày, truy vấn reminder sắp đến. | 19/11/2025 | 19/11/2025 | Proposal – DynamoDB Modeling |
| **Thu** | - Tham dự sự kiện AWS để cập nhật kiến thức về cloud-native & serverless. | 20/11/2025 | 20/11/2025 | — |
| **Fri** | - Thiết kế bảo mật & xác thực: Cognito User Pool, auth flow, JWT, API Gateway Authorizer.<br>- Hoàn thành tài liệu **Architecture Design v1** và gửi mentor/team để nhận feedback. | 21/11/2025 | 21/11/2025 | Proposal – Security & Authentication Sections |

---

### Week 10 Achievements

* Hoàn thiện **business requirements** và **user stories** cho Aurora Time.  
* Xây dựng được bản **kiến trúc serverless mức high-level**, gồm toàn bộ các dịch vụ chính của hệ thống.  
* Thiết kế **mô hình DynamoDB** đầy đủ, đảm bảo hỗ trợ tất cả access patterns của backend.  
* Xây dựng nền tảng **bảo mật & xác thực** với Cognito + API Gateway Authorizer.  
* Hoàn thành tài liệu **Architecture Design v1** – nền tảng cho quá trình implement thực tế.  
* Thu nhận thêm kiến thức tại sự kiện AWS, hỗ trợ hoàn thiện giải pháp theo best practices.

---
