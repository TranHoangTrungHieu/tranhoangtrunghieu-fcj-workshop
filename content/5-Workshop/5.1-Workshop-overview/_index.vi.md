---
title : "Giới thiệu"
date : "2025-09-09T19:53:52+07:00"
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Giới thiệu về Aurora Time

+ **Aurora Time** là một ứng dụng quản lý thời gian cá nhân, được xây dựng hoàn toàn trên kiến trúc **serverless** của AWS. Ứng dụng tập trung vào hai nhóm chức năng chính: quản lý lịch (events, schedules) và gửi nhắc việc tự động (reminders) qua email.
+ Hệ thống sử dụng các dịch vụ managed của AWS như **Amazon API Gateway**, **AWS Lambda**, **Amazon DynamoDB**, **Amazon EventBridge**, **Amazon SES**, **Amazon Cognito**, **AWS Amplify**, **Amazon S3** và **CloudFront** để đạt được khả năng mở rộng linh hoạt, độ sẵn sàng cao và chi phí vận hành rất thấp.[web:111][web:282]

#### Mục tiêu của workshop

Trong workshop này, bạn sẽ triển khai một phiên bản rút gọn của Aurora Time theo đúng kiến trúc đã đề xuất trong proposal của nhóm:

+ Xây dựng **backend serverless** với API Gateway + Lambda + DynamoDB để xử lý CRUD cho sự kiện, lịch và nhắc việc.
+ Cấu hình **EventBridge + SES** để gửi email nhắc việc tự động dựa trên thời gian người dùng đặt.
+ Thiết lập **Cognito User Pool** để đăng ký/đăng nhập người dùng và bảo vệ API bằng JWT.
+ Triển khai **frontend** (React hoặc framework tương đương) bằng **AWS Amplify**, lưu trữ tĩnh trên **S3/CloudFront**, kết nối trực tiếp tới API và Cognito.[web:111][web:281]

#### Tổng quan kiến trúc Aurora Time

Kiến trúc của Aurora Time được tổ chức xoay quanh các thành phần:

+ **Frontend**: Ứng dụng web tĩnh được build và host bởi **AWS Amplify**, phân phối qua **Amazon S3 + CloudFront** tới người dùng cuối.
+ **Lớp API & Logic**: **Amazon API Gateway** nhận request từ frontend, chuyển tiếp tới các hàm **AWS Lambda** để xử lý nghiệp vụ (tạo/sửa/xoá sự kiện, lấy danh sách lịch theo ngày/tuần/tháng, cấu hình reminder) và ghi/đọc dữ liệu từ **DynamoDB**.[web:282][web:283]
+ **Nhắc việc & Email**: **Amazon EventBridge Scheduler/Rules** lập lịch và kích hoạt Lambda gửi email thông qua **Amazon SES**, bảo đảm người dùng nhận được nhắc việc đúng thời điểm.[web:254][web:259]
+ **Bảo mật & Nhận diện**: **Amazon Cognito** quản lý tài khoản người dùng, phát hành JWT để API Gateway xác thực và phân quyền truy cập.

![Aurora Time – kiến trúc tổng thể](/images/aurora-time/architecture.png)
