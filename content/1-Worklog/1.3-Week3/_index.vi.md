---
title: "Worklog Tuần 3"
date: "2025-09-09T19:53:52+07:00"
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### 🎯 Mục tiêu tuần 3

* Hiểu các dịch vụ nâng cao thuộc nhóm Database và Compute trong AWS.  
* Thực hành triển khai Amazon RDS và EC2 Auto Scaling trong cùng kiến trúc VPC của tuần trước.  
* Bắt đầu tư duy xây dựng hạ tầng có khả năng mở rộng (scalable) và tính sẵn sàng cao (high availability).

---

### 📝 Công việc thực hiện trong tuần

| Ngày | Nhiệm vụ | Bắt đầu | Hoàn thành | Tài liệu |
|------|----------|-----------|-------------|-----------|
| **Thứ 2** | - Học kiến thức nền tảng về Amazon RDS: DB instance, engine, storage, Multi-AZ, backup, security group cho DB.<br>- Xem lại các kiến trúc phổ biến sử dụng RDS trong ứng dụng web. | 22/09/2025 | 22/09/2025 | https://www.youtube.com/watch?v=TQFwQAre0H4 |
| **Thứ 3** | - Thực hành tạo RDS instance trong cùng VPC với EC2 web server từ Tuần 2.<br>- Cấu hình Security Group để chỉ EC2 (hoặc private subnet ứng dụng) được phép truy cập DB. | 23/09/2025 | 23/09/2025 | https://www.youtube.com/watch?v=SlP-KdSs3IM |
| **Thứ 4** | - Tìm hiểu về EC2 Auto Scaling: Launch Template, Auto Scaling Group (ASG), Health Checks, scaling policies.<br>- Thiết kế một chính sách scaling đơn giản dựa trên CPU utilization. | 24/09/2025 | 24/09/2025 | https://www.youtube.com/watch?v=hFVYG8WqfU0 |
| **Thứ 5** | - Triển khai Auto Scaling Group trải trên ít nhất hai Availability Zones.<br>- Kiểm thử hành vi scale-out / scale-in bằng cách tăng tải hoặc giảm threshold. | 25/09/2025 | 25/09/2025 | https://000006.awsstudygroup.com |
| **Thứ 6** | - Tham dự một sự kiện AWS để bổ sung kiến thức thực tế và cập nhật xu hướng mới. | 26/09/2025 | 26/09/2025 | — |

---

### ⭐ Kết quả đạt được tuần 3

* Nắm vững kiến thức nền tảng về **Amazon RDS**, hiểu cách lựa chọn engine, storage, cấu hình Multi-AZ và backup.
* Triển khai thành công một **RDS instance** và cấu hình bảo mật đúng chuẩn (chỉ EC2 trong VPC được truy cập).
* Hiểu được kiến trúc web 2-tier: Web server (EC2) + Database tier (RDS).
* Làm chủ kiến thức **EC2 Auto Scaling**, bao gồm:
  * Launch Template  
  * Auto Scaling Group  
  * Scaling policies  
  * Health checks  
* Tạo được Auto Scaling Group trải rộng trên nhiều AZ để tăng tính sẵn sàng.
* Kiểm tra thành công cơ chế tự động scale-out và scale-in theo CPU utilization.
* Củng cố kỹ năng thiết kế hạ tầng linh hoạt và tiết kiệm chi phí theo triết lý “scale on demand”.
* Tư duy tốt hơn trong việc kết hợp nhiều dịch vụ AWS để tạo thành một kiến trúc hoàn chỉnh.

---

