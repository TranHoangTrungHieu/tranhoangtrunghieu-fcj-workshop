---
title: "Worklog Tuần 5"
date: "2025-09-09T19:53:52+07:00"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

### 🎯 Mục tiêu Tuần 5

* Hiểu cơ chế hoạt động của **AWS Storage Gateway** và cách dịch vụ này kết nối môi trường on-prem với AWS Cloud.  
* Thực hành đầy đủ quy trình triển khai: tạo S3 bucket → tạo EC2 làm máy chủ Gateway → kích hoạt và cấu hình Storage Gateway.  
* Nắm được các trường hợp sử dụng thực tế: hybrid storage, backup, archiving, file caching.

---

## 📝 Công việc đã thực hiện trong tuần (AWS Storage Gateway Module)

| Ngày | Nhiệm vụ | Bắt đầu | Hoàn thành | Tài liệu |
|------|-----------|-----------|-------------|-----------|
| **Thứ 2** | - Học lý thuyết về AWS Storage Gateway và 3 loại gateway (File, Volume, Tape).<br>- Hiểu kiến trúc lab: EC2 đóng vai trò gateway + S3 làm backend storage.<br>- Ghi chú các trường hợp doanh nghiệp thường dùng Storage Gateway. | 13/10/2025 | 13/10/2025 | https://www.youtube.com/watch?v=Je2jPk7HhLQ |
| **Thứ 3** | - Tạo S3 bucket dùng cho Storage Gateway lab.<br>- Cấu hình các thuộc tính: tên bucket, region, mã hóa (nếu cần), tags. | 14/10/2025 | 14/10/2025 | https://www.youtube.com/watch?v=3vSrTeWroSs |
| **Thứ 4** | - Tạo EC2 instance để chạy Storage Gateway appliance.<br>- Cấu hình networking và Security Group để EC2 có thể kết nối đến S3 và dịch vụ Storage Gateway an toàn (chỉ mở port cần thiết). | 15/10/2025 | 15/10/2025 | https://www.youtube.com/watch?v=xVrhpe8OpVU |
| **Thứ 5** | - Kích hoạt AWS Storage Gateway và gắn với S3 bucket đã tạo trước đó.<br>- Chọn đúng loại gateway theo yêu cầu lab (File hoặc Volume Gateway).<br>- Xác minh trạng thái gateway chuyển sang **ACTIVE**. | 16/10/2025 | 16/10/2025 | https://www.youtube.com/watch?v=Je2jPk7HhLQ |
| **Thứ 6** | - Kiểm tra hoạt động end-to-end: mount file share/volume, đọc/ghi dữ liệu, xác minh dữ liệu đã đồng bộ lên S3.<br>- Viết ghi chú nội bộ: “Cách AWS Storage Gateway kết nối workload on-prem với S3 và khi nào nên sử dụng trong dự án thực tế.” | 17/10/2025 | 17/10/2025 | https://www.youtube.com/watch?v=3Zp9GSMO-VI |

---

### ⭐ Kết quả đạt được Tuần 5

* Hiểu rõ kiến trúc và cơ chế hoạt động của **AWS Storage Gateway** trong bài toán hybrid storage.  
* Tạo và cấu hình thành công **S3 bucket** dùng làm backend storage.  
* Triển khai EC2 làm **máy chủ Storage Gateway**, cấu hình mạng và bảo mật đúng chuẩn.  
* Kích hoạt và cấu hình Storage Gateway kết nối với S3, gateway hoạt động ổn định (ACTIVE).  
* Kiểm thử thành công quy trình đọc/ghi dữ liệu và đồng bộ dữ liệu lên S3.  
* Hiểu được giá trị thực tế của Storage Gateway trong doanh nghiệp: backup, archiving, hybrid file storage.  
* Tăng cường kỹ năng thiết kế giải pháp hybrid giữa on-prem và AWS Cloud.

---
