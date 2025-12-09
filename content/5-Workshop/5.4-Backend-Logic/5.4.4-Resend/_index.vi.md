---
title: "Cấu hình Resend & Route 53"
date: 2025-12-09
weight: 1
chapter: false
pre: " <b> 5.4.0. </b> "
---

{{% notice info %}}
📧 **Mục tiêu:** Trước khi viết code gửi mail, chúng ta cần xác thực tên miền (Domain Verification) để đảm bảo email gửi đi không bị rơi vào Spam. Chúng ta sẽ kết nối **Resend** với **AWS Route 53**.
{{% /notice %}}

# Bước 1: Thêm Domain vào Resend

1. Truy cập [Resend Dashboard](https://resend.com/domains).
2. Bấm **Add Domain**.
3. Nhập tên miền của bạn:auroratime.click.
4. Chọn **Region** 
5. Bấm **Add**. Resend sẽ cung cấp cho bạn 3 loại bản ghi DNS (MX, SPF, DKIM).

> **Hình ảnh:**
> ![Screenshot: Bảng DNS Records do Resend cung cấp](images/resend-dns-records.png)

# Bước 2: Cấu hình DNS trên AWS Route 53

Chúng ta cần copy các bản ghi từ Resend và dán vào Route 53.

1. Truy cập **AWS Console** > **Route 53** > **Hosted zones**.
2. Chọn tên miền của bạn.
3. Bấm **Create record**.
4. **Tạo bản ghi MX (Mail Exchange):**
    * **Record name:** (Để trống hoặc theo hướng dẫn Resend)
    * **Record type:** MX
    * **Value:** Copy từ Resend 
5. **Tạo bản ghi TXT (SPF & DKIM):**
    * Làm tương tự cho các bản ghi TXT mà Resend yêu cầu.
    * *Lưu ý:* Nếu Record name có đuôi là domain , trong Route 53 bạn chỉ cần điền `bounces` (vì Route 53 tự điền đuôi domain).

> **Hình ảnh:**
> ![Screenshot: Tạo Record trong Route 53](images/route53-create-record.png)

# Bước 3: Xác thực và Lấy API Key

1. Quay lại Resend, bấm nút **Verify DNS Records**.
2. Đợi khoảng 1-5 phút để trạng thái chuyển sang **Verified** (Màu xanh).
3. Vào mục **API Keys** > **Create API Key**.
4. Đặt tên  và chọn quyền **Sending access**.
5. **Copy và lưu trữ API Key này cẩn thận** (Chúng ta sẽ dùng nó trong code Lambda ở các bài sau).

> **Hình ảnh:**
> ![Screenshot: Resend báo Verified thành công](images/resend-verified.png)

{{% notice tip %}}
💡 **Lưu ý:** Việc cấu hình này giúp tăng độ uy tín (Reputation) cho domain của bạn, đảm bảo email thông báo từ hệ thống Aurora sẽ vào **Inbox** thay vì **Spam**.
{{% /notice %}}