---
title: "Workshop"
date: 2025-12-09
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

{{% notice info %}}
💡 **Thông tin dự án:** Aurora là hệ thống quản lý sự kiện và tự động hóa thông báo, được xây dựng trên kiến trúc Serverless.
{{% /notice %}}

# Project Aurora: Hệ thống Quản lý Sự kiện & Thông báo Tự động

#### Tổng quan dự án

**Project Aurora** là giải pháp giúp người dùng quản lý lịch trình, tạo các sự kiện quan trọng và theo dõi danh sách việc làm hằng ngày (Daily Worklog). Điểm đặc biệt của hệ thống là khả năng tích hợp **thông báo tự động qua Email** để nhắc nhở người dùng khi đến giờ sự kiện.

Trong dự án này, chúng ta sẽ tập trung giải quyết bài toán về tạo lịch  và gửi thông báo tin cậy (Reliable Notifications) mà không cần duy trì máy chủ liên tục.

Các tính năng và dịch vụ chính:
+ **Amazon Cognito & Google Cloud:** Quản lý định danh người dùng (Identity), cấu hình **Google Sign-In** (OAuth 2.0) giúp đăng nhập an toàn và tiện lợi.
+ **Quản lý Sự kiện & Task:** Sử dụng **Amazon DynamoDB** để lưu trữ thông tin sự kiện và trạng thái công việc hàng ngày.
+ **Gửi Email thông báo:** Tích hợp **Resend**  để gửi email nội dung HTML đẹp mắt đến người dùng.
+ **Xử lý Logic:** Sử dụng **AWS Lambda** để xử lý luồng dữ liệu khi tạo sự kiện mới.
 ![Aurora Time Platform Architecture](/AWS/images/2-Proposal/aws.jpg)
#### Nội dung chi tiết

1. [Kiến trúc hệ thống & Luồng xác thực (Auth Flow)](5.1-Architecture/)
2. [Cấu hình Google Cloud & Amazon Cognito](5.2-Auth-Setup/)
3. [Thiết kế Database (Events & Tasks)](5.3-Database/)
4. [Xây dựng API & Logic gửi Mail (Lambda)](5.4-Backend-Logic/)
5. [Giao diện người dùng (Frontend)](5.5-Frontend/)
6. [Kết quả và Hướng phát triển](5.6-Conclusion/)