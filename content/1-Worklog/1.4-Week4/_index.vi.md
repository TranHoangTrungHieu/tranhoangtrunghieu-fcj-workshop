---
title: "Worklog Tuần 4"
date: "2025-09-09T19:53:52+07:00"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### 🎯 Mục tiêu Tuần 4

* Nắm vững các kiến thức Networking nâng cao trong AWS, đặc biệt là Hybrid DNS với Route 53 Resolver.  
* Hiểu cách AWS kết nối với môi trường on-prem thông qua DNS forwarding và Transit Gateway.  
* Tăng cường tư duy bảo mật thông qua cấu hình Security Group đúng nguyên tắc least-privilege.

---

### 📝 Công việc đã thực hiện trong tuần

| Ngày | Nhiệm vụ | Bắt đầu | Hoàn thành | Tài liệu |
|------|-----------|-----------|-------------|-----------|
| **Thứ 2** | - Học lý thuyết về Hybrid DNS: Route 53 Resolver, inbound/outbound endpoints, forwarding rules, mô hình DNS giữa on-prem và AWS.<br>- Ghi chú lại các mô hình Hybrid DNS thường được doanh nghiệp áp dụng. | 06/10/2025 | 06/10/2025 | https://www.youtube.com/watch?v=FGicpWOmMDI |
| **Thứ 3** | - Thực hành lab Hybrid DNS: tạo các VPC, subnet, và cấu hình Route 53 ban đầu.<br>- Vẽ sơ đồ kiến trúc gồm DNS on-prem, Route 53 Resolver, inbound/outbound endpoints và VPCs. | 07/10/2025 | 07/10/2025 | https://000010.awsstudygroup.com/vi/ |
| **Thứ 4** | - Cấu hình Security Groups cho môi trường Hybrid DNS: chỉ cho phép ICMP (ping) và RDP để test, loại bỏ các port không cần thiết theo nguyên tắc least-privilege.<br>- Kiểm tra kết nối để đảm bảo các rule hoạt động đúng. | 08/10/2025 | 08/10/2025 | https://www.youtube.com/watch?v=kE_krznNBFU |
| **Thứ 5** | - Hoàn tất cấu hình Hybrid DNS: tạo inbound/outbound Resolver endpoints và các Resolver rules để forward domain giữa on-prem và AWS.<br>- Kiểm tra khả năng phân giải DNS 2 chiều: từ on-prem → AWS và từ AWS → on-prem. | 09/10/2025 | 09/10/2025 | https://www.youtube.com/watch?v=L-2YfZceoAU |
| **Thứ 6** | - Học về AWS Transit Gateway: khái niệm, attachments, routing, mô hình giá.<br>- Tạo Transit Gateway, gắn VPCs vào TGW và cập nhật route table để bật kết nối liên VPC; kiểm tra cross-VPC connectivity. | 10/10/2025 | 10/10/2025 | https://www.youtube.com/watch?v=W1m_OFPDui0 |

---

### ⭐ Kết quả đạt được Tuần 4

* Hiểu rõ cách hoạt động của **Hybrid DNS** trong môi trường doanh nghiệp.  
* Cấu hình thành công **Route 53 Resolver inbound/outbound endpoints** và các forwarding rules.  
* Nâng cao tư duy bảo mật nhờ cấu hình **Security Group theo nguyên tắc least-privilege**.  
* Thiết lập và vận hành **Transit Gateway**, kết nối nhiều VPC lại với nhau thông qua định tuyến tập trung.  
* Thực hành kiểm thử và xử lý lỗi liên quan đến DNS forwarding và network routing.  
* Tăng cường kiến thức về networking nâng cao trong AWS, tạo nền tảng cho các lab tiếp theo như Site-to-Site VPN và Direct Connect.

---
