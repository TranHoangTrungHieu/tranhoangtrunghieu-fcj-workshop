---
title: "Bản đề xuất"
date: "2025-09-09T19:53:52+07:00"
weight: 2
chapter: false
pre: "<b> 2. </b>"
---


## **Aurora Time**

---

### **Tóm tắt điều hành**
Bản đề xuất này trình bày kế hoạch triển khai **Aurora Time**, một ứng dụng quản lý thời gian trên nền tảng AWS.  
Mục tiêu là cung cấp công cụ lập lịch đơn giản, trực quan và tiết kiệm chi phí cho người dùng cá nhân.  

Aurora Time tận dụng các dịch vụ **Serverless** và **Managed Services** của AWS để đạt được khả năng mở rộng, độ tin cậy cao, và tối ưu chi phí — mang lại **lợi tức đầu tư (ROI)** nhanh chóng nhờ loại bỏ gánh nặng vận hành hạ tầng.

---

### **Tuyên bố vấn đề**

#### **Vấn đề hiện tại**
Người dùng gặp khó khăn trong việc quản lý lịch trình cá nhân vì thông tin bị phân tán giữa nhiều công cụ (ghi chú, điện thoại, app khác nhau).  
Các giải pháp hiện có thường quá phức tạp, thiên về doanh nghiệp, không phù hợp với nhu cầu cá nhân.  

**Aurora Time** mang đến giải pháp **tập trung hóa, tối giản và trực quan**, giúp người dùng dễ dàng quản lý thói quen và sự kiện cá nhân.

#### **Giải pháp đề xuất**
Aurora Time sử dụng **Amazon S3** và **CloudFront** để lưu trữ & phân phối ứng dụng web, **AWS Amplify** để triển khai nhanh.  
**Amazon API Gateway** và **AWS Lambda** xử lý backend CRUD, **DynamoDB** lưu dữ liệu nhanh, ổn định.  
**Amazon Cognito** xác thực người dùng, **EventBridge** & **SES** gửi nhắc nhở tự động.  

**Tính năng chính:**
- Giao diện lập lịch trực quan  
- Nhắc nhở tùy chỉnh  
- Chi phí cực thấp  

---

### **Lợi ích và hoàn vốn đầu tư (ROI)**
Aurora Time giúp người dùng tiết kiệm thời gian, giảm phân tán lịch trình và tăng năng suất.  
- **Chi phí hạ tầng:** $16 – $50/tháng (~$192 – $600/năm)  
- **Hoàn vốn:** Dưới 6 tháng  
- **Ưu điểm:** Không cần máy chủ, chi phí cực thấp, dễ mở rộng  

---

### **Kiến trúc giải pháp**
Aurora Time áp dụng kiến trúc **AWS Serverless** cho phép mở rộng linh hoạt từ một đến hàng triệu người dùng.  
Các yêu cầu được tiếp nhận qua **Amazon API Gateway**, xử lý bởi **AWS Lambda**, lưu trữ trong **DynamoDB**.  
**EventBridge** lên lịch và kích hoạt nhắc nhở, **AWS Amplify** cung cấp giao diện, bảo mật bởi **Cognito**.

![Kiến trúc AWS Serverless của Aurora Time](/images/2-Proposal/aurora-architecture.jpeg)

---

### **Dịch vụ AWS sử dụng**

| Dịch vụ AWS | Chức năng |
|--------------|------------|
| **AWS Lambda** | Xử lý logic nghiệp vụ CRUD và nhắc nhở. |
| **Amazon API Gateway** | Cung cấp API RESTful an toàn. |
| **Amazon DynamoDB** | Lưu trữ dữ liệu lịch, sự kiện, người dùng. |
| **Amazon S3 & CloudFront** | Lưu trữ và phân phối nội dung frontend. |
| **Amazon EventBridge** | Lên lịch và kích hoạt sự kiện tự động. |
| **Amazon SES** | Gửi email nhắc nhở người dùng. |
| **AWS Amplify** | Lưu trữ và quản lý frontend. |
| **Amazon Cognito** | Xác thực & quản lý người dùng an toàn. |

### **Kế hoạch triển khai kỹ thuật**

1. **Tháng 1 – Nghiên cứu & Thiết kế kiến trúc:**  
   DynamoDB modeling, kiến trúc Serverless (API Gateway, Lambda, EventBridge).  
2. **Tháng 1 – POC & Ước tính chi phí:**  
   AWS Pricing Calculator, kiểm thử Cognito + DynamoDB.  
3. **Tháng 2 – Tối ưu hệ thống:**  
   Tinh chỉnh Lambda (timeout, memory), tối ưu RCU/WCU DynamoDB.  
4. **Tháng 2–3 – Phát triển & CI/CD:**  
   Xây dựng Lambda functions, thiết lập CodePipeline + CodeBuild, phát triển React UI, kiểm thử Beta.  

---

### **Chi phí hạ tầng ước tính**

| Dịch vụ | Mô tả | Chi phí/tháng (USD) |
|----------|--------|--------------------|
| AWS Amplify | Lưu trữ web tĩnh | 0.35 |
| S3 | File tĩnh & backup | 0.05 |
| CloudFront | CDN (20GB) | 1.70 |
| API Gateway | 30.000 yêu cầu | 0.11 |
| Lambda | 1M yêu cầu (free tier) | 0.00 |
| DynamoDB | 1GB dữ liệu (free tier) | 0.11 |
| Cognito | <1000 người dùng | 0.00 |
| SES | 500 email/tháng | 0.05 |
| EventBridge | 100k event | 0.10 |
| CloudWatch Logs | 1GB log | 0.10 |
| CI/CD Pipeline | 20 build | 0.00 |

👉 **Tổng chi phí:** ~ $16 – $50/tháng (~$192 – $600/năm)

---

### **Rủi ro & Giảm thiểu**

| Rủi ro | Ảnh hưởng | Xác suất | Giảm thiểu |
|--------|------------|-----------|-------------|
| Mất kết nối mạng | Trung bình | Trung bình | Dùng cache & CDN (CloudFront). |
| Lỗi DynamoDB | Cao | Trung bình | Thực hiện POC & load test. |
| Chi phí vượt ngân sách | Trung bình | Thấp | Thiết lập AWS Budgets cảnh báo. |
| Lỗi EventBridge/Lambda | Cao | Thấp | Theo dõi CloudWatch & retry logic. |

---

### **Kết quả kỳ vọng**
- Trải nghiệm lập lịch dễ dùng, trực quan, nhắc nhở tự động.  
- Hệ thống serverless ổn định, chi phí cực thấp, dễ mở rộng.  
- Hoàn thành triển khai trong thời gian thực tập, có CI/CD tự động.