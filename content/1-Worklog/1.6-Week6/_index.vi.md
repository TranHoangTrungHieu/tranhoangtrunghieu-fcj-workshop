---
title: "Worklog Tuần 6"
date: "2025-09-09T19:53:52+07:00"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### 🎯 Mục tiêu Tuần 6

* Hiểu sâu hơn về Amazon S3 và các tính năng phục vụ lưu trữ theo quy mô lớn.  
* Nắm được cách tối ưu chi phí, bảo mật và hiệu năng khi thiết kế hệ thống sử dụng S3.  
* Thực hành các cấu hình quan trọng: Static Website Hosting, CORS, Versioning, Storage Class.

---

## 📝 Công việc đã thực hiện trong tuần

| Ngày | Nhiệm vụ | Bắt đầu | Hoàn thành | Tài liệu |
|------|-----------|----------|------------|-----------|
| **Thứ 2** | - Nghỉ ngơi, không có lab mới. | 20/10/2025 | 20/10/2025 | — |
| **Thứ 3** | - Xem video **Module 04-02 – Amazon S3 – Access Point – Storage Class**.<br>- Ghi chú về: S3 Access Points, lợi ích khi chia nhỏ quyền truy cập theo từng nhóm người dùng/dataset.<br>- Tìm hiểu chi tiết Storage Classes và cách tối ưu chi phí theo tần suất truy cập. | 21/10/2025 | 21/10/2025 | https://www.youtube.com/watch?v=_yunukwcAwc |
| **Thứ 4** | - Xem video **Module 04-03 – S3 Static Website, CORS, Object Key, Glacier**.<br>- Hiểu cơ chế hosting website tĩnh trên S3.<br>- Thực hành phân tích CORS, ACL, IAM Policies và object key design để tối ưu hiệu năng.<br>- Tìm hiểu nhóm Glacier và các tùy chọn phục hồi dữ liệu (retrieval). | 22/10/2025 | 22/10/2025 | https://www.youtube.com/watch?v=mPBjB6Ltl_Q |
| **Thứ 5** | - Xem video **Module 04-04 – S3 Versioning & Data Protection**.<br>- Thực hành bật Versioning trên bucket thử nghiệm.<br>- Upload nhiều phiên bản object, test delete/restore để hiểu cách Versioning bảo vệ dữ liệu trước lỗi ghi đè hoặc xóa nhầm. | 23/10/2025 | 23/10/2025 | https://www.youtube.com/watch?v=YXn8Q_Hpsu4 |
| **Thứ 6** | - Nghỉ ngơi, không có lab mới. | 24/10/2025 | 24/10/2025 | — |

---

### ⭐ Kết quả đạt được trong Tuần 6

* Hiểu rõ **S3 Access Points** và lý do chúng giúp đơn giản hóa quyền truy cập trong môi trường multi-tenant hoặc big data.  
* Nắm được toàn bộ hệ thống **S3 Storage Classes**, bao gồm cách lựa chọn lớp lưu trữ tối ưu chi phí theo workload.  
* Hiểu và có thể triển khai **S3 Static Website Hosting**, bao gồm cấu hình CORS đúng để tránh lỗi truy cập từ frontend.  
* Nắm sự khác biệt giữa **ACL – IAM Policy – Resource Policy** và khi nào nên dùng từng loại.  
* Hiểu cách thiết kế **object key** để cải thiện hiệu năng và giảm chi phí trả về dữ liệu.  
* Thực hành với **S3 Versioning**, bao gồm: tạo phiên bản file, xóa nhầm, khôi phục version trước đó.  
* Hiểu Glacier và các lớp lưu trữ dành cho archival, cũng như thời gian phục hồi dữ liệu.  
* Hoàn thiện kiến thức quan trọng để chuẩn bị cho các module chuyên sâu hơn về CloudFront, Route 53, và kiến trúc phân phối nội dung.

---
