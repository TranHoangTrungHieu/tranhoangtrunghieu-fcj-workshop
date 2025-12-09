---
title : "Thiết kế & tạo bảng DynamoDB"
date : "2025-09-09T19:53:52+07:00"
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

Trong phần này, bạn sẽ tạo bảng **DynamoDB** dùng để lưu trữ các sự kiện (events) của người dùng Aurora Time.  
Bảng này là nền tảng cho toàn bộ chức năng tạo/lấy/sửa/xoá lịch và nhắc việc.

1. Mở **DynamoDB console** trong region mà bạn triển khai Aurora Time.

2. Ở thanh điều hướng bên trái, chọn **Tables**, sau đó click **Create table**.

{{% notice note %}}
Aurora Time sử dụng kiến trúc serverless nên DynamoDB là lựa chọn phù hợp cho lưu trữ dữ liệu sự kiện với độ trễ thấp, khả năng mở rộng tự động và chi phí thấp.
{{% /notice %}}

![Tạo bảng DynamoDB](/images/aurora-time/dynamodb-create-table.png)

3. Trong màn hình **Create table**:

   + **Table name**: `AuroraTimeEvents`  
   + **Partition key**: `userId` (Type: String) – dùng để phân vùng dữ liệu theo từng người dùng.  
   + **Sort key**: `eventKey` (Type: String) – dùng để lưu giá trị dạng `eventId#yyyy-mm-dd`, giúp dễ truy vấn theo sự kiện và ngày.

![Khai báo key schema](/images/aurora-time/dynamodb-events-key-schema.png)

4. Ở phần **Table settings**:

   + Chọn **Use default settings** hoặc chỉnh sang **On‑demand capacity** (Recommended) để không phải tự tính RCU/WCU trong giai đoạn POC.
   + Giữ nguyên các tuỳ chọn backup, encryption ở mức mặc định cho workshop.

![Cấu hình capacity](/images/aurora-time/dynamodb-events-capacity.png)

5. Cuộn xuống cuối trang, click **Create table** và chờ đến khi trạng thái bảng là **Active**.

![Bảng AuroraTimeEvents đã được tạo](/images/aurora-time/dynamodb-events.png)

6. (Tuỳ chọn) Thêm một vài item mẫu để kiểm thử:

   + `userId`: `demo-user-1`  
   + `eventKey`: `event-001#2025-09-10`  
   + Các thuộc tính khác: `title`, `startTime`, `endTime`, `reminderOffset`, `status`, …

![Thêm dữ liệu mẫu](/images/aurora-time/dynamodb-events-items.png)

Bạn đã tạo xong bảng **AuroraTimeEvents**. Ở các bước tiếp theo, các Lambda function như `CreateEvent`, `ListEvents`, `UpdateEvent` và `DeleteEvent` sẽ sử dụng bảng này để thao tác dữ liệu lịch và nhắc việc cho từng người dùng.
