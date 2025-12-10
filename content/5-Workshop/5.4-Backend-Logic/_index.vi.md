---
title: "Xây dựng API & Logic gửi Mail "
date: 2025-12-09
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

{{% notice info %}}
🛡️ **Mục tiêu:** Xây dựng Backend Serverless theo quy trình 4 bước: Tạo Function -> Cấu hình Role -> Cấp quyền Database -> Lập trình xử lý (Kết nối DB & Gọi API Mail bên thứ 3).
{{% /notice %}}

# Bước 1: Khởi tạo Lambda Function

Đầu tiên, chúng ta tạo một hàm Lambda mới để làm nơi chứa logic xử lý.

1. Truy cập **AWS Console** > **Lambda** > **Create function**.
2. **Function name:** .
3. **Runtime:** Chọn **Node.js 18.x** (hoặc 20.x).
4. **Architecture:** x86_64.
5. Giữ nguyên các cài đặt mặc định khác và bấm **Create function**.

> **Hình ảnh thực hiện:**
>
> ![Screenshot: Màn hình khởi tạo Lambda Function](/AWS/images/5-Workshop/lambda.png)
> *Hình 5.4.1: Khởi tạo hàm xử lý Backend.*

---
# Bước 2: Add Policies cho Lambda (Execution Role)

Mặc định khi tạo, Lambda sẽ tự động tạo một IAM Role cơ bản. Chúng ta cần truy cập vào Role này để cấp quyền ghi dữ liệu vào Database.

1. Trong giao diện Lambda vừa tạo, chuyển sang tab **Configuration**.
2. Chọn mục **Permissions** ở cột bên trái.
3. Bấm vào tên Role dưới mục **Execution role**  để mở sang trang IAM Console.

> **Hình ảnh thực hiện:**
>
> ![Screenshot: Truy cập vào Execution Role từ Lambda](/AWS/images/5-Workshop/role.png)
> *Hình 5.4.2: Truy cập IAM Role để cấu hình quyền hạn.*
> # Bước 3: Add Policies để kết nối DB

Vì chúng ta sử dụng dịch vụ Email bên thứ 3 (gọi qua API HTTP thông thường), nên **không cần** cấp quyền SES nữa. Chúng ta chỉ cần cấp quyền cho Lambda làm việc với **DynamoDB**.

1. Tại tab **Permissions** của Role, bấm nút **Add permissions** > **Create inline policy**.
2. Chọn chế độ **JSON**
3. Bấm Next, đặt tên Policy là AuroraDB_Access_Policy và bấm Create policy
4. Kiểm tra lại danh sách Permissions, đảm bảo Role đã có quyền truy cập DynamoDB
![Screenshot: Truy cập vào add policy từ Lambda](/AWS/images/5-Workshop/permission.png)
> *Hình 5.4.2:  cấu hình policy.*
# Bước 4: Viết Code cho hàm Lambda
Quay trở lại giao diện Lambda Function, chúng ta sẽ viết code Node.js.
![Screenshot: Truy cập vào để viết code](/AWS/images/5-Workshop/code.png)
Sau khi hoàn thành, bấm **Deploy** để lưu lại.