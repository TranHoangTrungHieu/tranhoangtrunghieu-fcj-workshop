---
title: "Kiến trúc hệ thống & Luồng xác thực (Auth Flow)"
date: 2025-12-09
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

{{% notice note %}}
📋 **Nội dung:** Phần này mô tả thiết kế High-level của hệ thống Aurora và chi tiết luồng xác thực người dùng thông qua Google (OAuth 2.0) kết hợp với Amazon Cognito.
{{% /notice %}}

# 1. Sơ đồ kiến trúc tổng quan (High-Level Architecture)

Hệ thống **Aurora** được thiết kế theo kiến trúc **Serverless** hoàn toàn trên AWS, giúp tối ưu chi phí vận hành và khả năng mở rộng. Hệ thống tích hợp với **Google Cloud Platform** để cung cấp trải nghiệm đăng nhập liền mạch (Single Sign-On).

![Sơ đồ kiến trúc Aurora](/AWS/images/2-Proposal/aws.jpg)

### Các thành phần chính:

1.  **Frontend (Client):** Ứng dụng Web (SPA) nơi người dùng tương tác, xem lịch và tạo task.
2.  **Authentication Layer:**
    * **Google Cloud Project:** Cung cấp OAuth 2.0 Client ID/Secret để xác thực danh tính người dùng Gmail.
    * **Amazon Cognito:** Đóng vai trò là Identity Provider (IdP) trung gian, quản lý User Pool và cấp phát AWS Credentials tạm thời cho Frontend.
3.  **Backend Logic (Compute):**
    * **AWS Lambda:** Chứa các hàm xử lý logic nghiệp vụ (Tạo sự kiện, Cập nhật task, Trigger gửi mail).
4.  **Database:**
    * **Amazon DynamoDB:** Lưu trữ dữ liệu Events và Daily Worklogs. Sử dụng Partition Key là `UserId` để đảm bảo dữ liệu người dùng được cô lập.
5.  **Notification Service:**
    * **Logic gửi Mail:** Được kích hoạt bởi Lambda khi có sự kiện mới hoặc đến giờ hẹn, sử dụng dịch vụ Email (SES/Gmail API) để gửi thông báo đến người dùng.

---

# 2. Luồng xác thực (Authentication Flow)

Đây là quy trình quan trọng nhất để đảm bảo chỉ người dùng đã đăng nhập mới có quyền truy cập vào dữ liệu cá nhân của họ. Chúng ta sử dụng mô hình **Cognito Federated Identities** kết hợp với **Google**.

### Chi tiết các bước xử lý:

1.  **User Login:** Người dùng bấm nút "Sign in with Google" trên Frontend.
2.  **Google OAuth:** Frontend chuyển hướng người dùng sang trang đăng nhập của Google. Sau khi đăng nhập thành công, Google trả về một `Id Token` (JWT).
3.  **Exchange Token:** Frontend gửi `Id Token` này đến **Amazon Cognito**.
4.  **Verification & Session:** Amazon Cognito xác thực Token với Google. Nếu hợp lệ:
    * Cognito tạo (hoặc cập nhật) hồ sơ người dùng trong User Pool.
    * Cognito trả về bộ **AWS Temporary Credentials** (Access Key, Secret Key, Session Token) cho Frontend.
5.  **Authorized Request:** Frontend dùng bộ Credentials này để gọi trực tiếp các API (thông qua API Gateway hoặc gọi thẳng Lambda/DynamoDB nếu dùng SDK) với quyền hạn được quy định trong IAM Role.

---

# 3. Luồng dữ liệu: Tạo Sự kiện & Gửi Mail

Khi người dùng tạo một sự kiện mới (ví dụ: "Họp team lúc 9:00 AM"), luồng dữ liệu sẽ đi như sau:

1.  **Frontend** gửi request POST chứa thông tin sự kiện đến API Endpoint.
2.  **AWS Lambda** được kích hoạt (Trigger):
    * Validate dữ liệu đầu vào.
    * Ghi thông tin sự kiện vào bảng **DynamoDB** (Table: `AuroraEvents`).
3.  **Email Notification Trigger:**
    * Sau khi ghi DB thành công, Lambda tiếp tục gọi hàm gửi mail.
    * Hệ thống cấu hình nội dung mail HTML.
    * Gửi lệnh đến **Email Service** để chuyển thư tới hộp thư của người dùng.

{{% notice tip %}}
💡 **Điểm nổi bật:** Việc tích hợp Google Login giúp người dùng không cần nhớ thêm một mật khẩu mới cho hệ thống Aurora, đồng thời tận dụng được bảo mật 2 lớp từ Google.
{{% /notice %}}