---
title: "Thiết kế Database (DynamoDB)"
date: 2025-12-09
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

{{% notice info %}}
🗄️ **Mục tiêu:** Thiết kế cơ sở dữ liệu NoSQL với Amazon DynamoDB để lưu trữ Sự kiện (Events) và Công việc (Todo), tối ưu hóa cho truy xuất nhanh và chi phí thấp.
{{% /notice %}}

# 1. Tại sao chọn Amazon DynamoDB?

Với kiến trúc Serverless của dự án Aurora, **Amazon DynamoDB** là sự lựa chọn tối ưu vì:
* **Serverless:** Không cần quản lý máy chủ, tự động mở rộng (Auto-scaling) theo lưu lượng truy cập.
* **Hiệu năng cao:** Độ trễ thấp (single-digit millisecond), phù hợp cho các thao tác thời gian thực trên giao diện người dùng.
* **Linh hoạt (Schemaless):** Dễ dàng thay đổi cấu trúc dữ liệu (thêm trường mới cho Event/Todo) mà không cần migration phức tạp như SQL.

---

# 2. Thiết kế Schema (Data Modeling)

Hệ thống sử dụng mô hình **Per-User Isolation**. Mỗi item (bản ghi) đều gắn liền với một `userId` (Lấy từ Cognito/Google Token) để đảm bảo bảo mật.

Chúng ta sẽ tạo 2 bảng (Tables) chính:

### Bảng 1: AuroraEvents (Lưu trữ lịch trình)
Bảng này lưu các sự kiện lịch, phục vụ cho việc hiển thị trên Calendar và quét để gửi thông báo.

* **Partition Key (PK):** `userId` (String) - Định danh người dùng.
* **Sort Key (SK):** `eventId` (String) - UUID của sự kiện.

### Bảng 2: AuroraTasks (Lưu trữ công việc hàng ngày)
Bảng này lưu danh sách Daily Worklog (To-do list).

* **Partition Key (PK):** `userId` (String).
* **Sort Key (SK):** `todoId` (String) - UUID của công việc.

### Bảng 3: users (Lưu trữ thông tin người dùng)
Bảng này lưu thông tin chi tiết về người dùng.

* **Partition Key (PK):** `userId` (String).
---

# 3. Các bước khởi tạo trên AWS Console

Dưới đây là quy trình tạo bảng trên giao diện AWS.

### Bước 1: Tạo bảng Events
Truy cập **DynamoDB** > **Tables** > **Create table**.
* **Table name:** `events`
* **Partition key:** `userId` (String)
* **Sort key:** `eventId` (String)

> **Hình ảnh thực hiện:**
>
> ![Screenshot: Màn hình tạo bảng AuroraEvents](images/dynamodb-create-event.png)
> 

### Bước 2: Tạo bảng Tasks
Tương tự, tạo bảng thứ hai cho Task.
* **Table name:** `todo`
* **Partition key:** `userId` (String)
* **Sort key:** `todoId` (String)

> **Hình ảnh thực hiện:**
>
> ![Screenshot: Màn hình tạo bảng AuroraTasks](images/dynamodb-create-task.png)
> 
>
> ### Bước 3: Tạo bảng Users
Tương tự, tạo bảng thứ ba cho User.
* **Table name:** `users`
* **Partition key:** `userId` (String)

> **Hình ảnh thực hiện:**
>
> ![Screenshot: Màn hình tạo bảng AuroraTasks](images/dynamodb-create-task.png)
> 

}