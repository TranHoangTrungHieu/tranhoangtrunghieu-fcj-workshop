---
title: " Frontend & API Gateway"
date: 2025-12-09
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

{{% notice info %}}
🌐 **Kiến trúc:** Chúng ta sẽ xây dựng một hệ thống bảo mật tiêu chuẩn: Frontend (Amplify) -> API Gateway (có xác thực Cognito) -> Lambda Backend.
{{% /notice %}}

# Mô hình kết nối

Để đảm bảo tính bảo mật và quản lý tập trung, chúng ta không cho phép Frontend gọi trực tiếp Lambda. Thay vào đó, chúng ta sử dụng **Amazon API Gateway**.

Quy trình hoạt động:
1.  **Deploy:** Frontend ReactJS được host trên **AWS Amplify**.
2.  **Authenticate:** Người dùng đăng nhập qua Google/Cognito và nhận về `IdToken`.
3.  **Request:** Frontend gửi request đến **API Gateway** kèm theo `Authorization Header` chứa Token.
4.  **Authorize:** API Gateway kiểm tra Token với Cognito. Nếu hợp lệ -> Chuyển tiếp đến Lambda.
5.  **Execute:** Lambda thực thi logic và trả kết quả.