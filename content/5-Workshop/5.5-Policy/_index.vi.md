---
title : "Chính sách bảo mật & phân quyền API"
date : "2025-09-09T19:53:52+07:00"
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

Khi triển khai Aurora Time, ngoài việc xác thực bằng **Amazon Cognito**, bạn còn có thể áp dụng **chính sách bảo mật bổ sung** để kiểm soát chi tiết quyền truy cập vào API và dữ liệu.  
Tương tự như VPC Endpoint Policy với S3, ở đây chúng ta sẽ dùng **Cognito groups + API Gateway + IAM** để phân quyền chi tiết (fine‑grained authorization) cho các thao tác nhạy cảm, ví dụ xoá sự kiện (DELETE).[web:299][web:104]

Trong phần này, bạn sẽ:

+ Tạo hai nhóm quyền trong Cognito: `user` và `admin`.  
+ Giữ cho các API đọc/tạo sự kiện mở cho cả hai nhóm, nhưng chỉ cho phép nhóm `admin` gọi endpoint **DELETE /events/{id}**.  
+ Kiểm thử để xác nhận user thường bị từ chối, còn admin thực hiện được.

![Minh hoạ phân quyền theo nhóm Cognito](/images/aurora-time/api-policy-architecture.png)

---

#### Bước 1 – Tạo Cognito groups cho Aurora Time

1. Mở **Cognito console**, chọn **User pool** của Aurora Time.

2. Trong menu bên trái, chọn **Groups** → **Create group**:
   + Tạo group `user` (mặc định cho người dùng bình thường).  
   + Tạo group `admin` (dành cho tài khoản quản trị, được phép thao tác nhạy cảm như xoá sự kiện).

3. Gán:
   + Tài khoản test thứ nhất vào group `user`.  
   + Tài khoản test thứ hai vào group `admin`.

![Cognito groups](/images/aurora-time/cognito-groups.png)

---

#### Bước 2 – Cấu hình API Gateway sử dụng Cognito Authorizer

1. Mở **Amazon API Gateway console**, chọn REST API Aurora Time.

2. Trong tab **Authorizers**:
   + Tạo (hoặc kiểm tra) authorizer kiểu **Cognito** trỏ tới User Pool Aurora Time.  
   + Đảm bảo các method như `GET /events`, `POST /events`, `DELETE /events/{id}` đều sử dụng authorizer này.[web:104][web:308]

3. Ở method **DELETE /events/{id}**, vào **Method Request**:
   + Đảm bảo **Authorization** = Cognito authorizer.  
   + (Tuỳ chọn) Khai báo thêm `Authorization Scopes` nếu bạn dùng OAuth 2.0 scopes cho admin.

![API Gateway – DELETE /events/{id}](/images/aurora-time/apigw-delete-event.png)

---

#### Bước 3 – Hạn chế quyền xoá sự kiện cho admin

Để chỉ cho phép nhóm `admin` gọi `DELETE /events/{id}`, bạn có thể dùng một trong hai cách:

1. **Kiểm tra claim `cognito:groups` trong Lambda**  

   Trong hàm Lambda xử lý xoá sự kiện, đọc JWT từ `event.requestContext.authorizer.claims`:

const claims = event.requestContext.authorizer.claims;
const groups = claims['cognito:groups'] || '';

if (!groups.includes('admin')) {
return {
statusCode: 403,
body: JSON.stringify({ message: 'Access denied: admin only.' })
};
}

   Nếu user không thuộc group `admin`, Lambda trả về 403 và không gọi DynamoDB xoá dữ liệu.  
   Cách này đơn giản, dễ hiểu và phù hợp với kiến trúc Lambda backend hiện tại.[web:299]

2. **(Nâng cao) Dùng IAM policy/authorizer tuỳ chỉnh**  

   Bạn có thể viết Lambda authorizer hoặc IAM policy chi tiết hơn để API Gateway chỉ forward request tới Lambda khi claim `cognito:groups` là `admin`. Điều này giống với mô hình fine‑grained authorization mà AWS gợi ý trong các bài blog về Cognito + API Gateway + IAM.[web:299][web:310]

---

#### Bước 4 – Kiểm thử phân quyền

1. **Đăng nhập bằng user thường (group `user`):**

   + Vào Aurora Time, lấy token Cognito, gọi API `GET /events` (qua frontend hoặc Postman) → **thành công**.  
   + Thử xoá sự kiện bất kỳ qua `DELETE /events/{id}` → nhận **403 Forbidden** với thông báo “Access denied: admin only”.

![User thường bị chặn khi xoá sự kiện](/images/aurora-time/delete-event-user-fail.png)

2. **Đăng nhập bằng admin (group `admin`):**

   + Gọi lại `DELETE /events/{id}` với cùng sự kiện → request **thành công**, item bị xoá khỏi DynamoDB.  
   + Kiểm tra bảng `AuroraTimeEvents` trong DynamoDB để xác nhận sự kiện không còn tồn tại.

![Admin xoá sự kiện thành công](/images/aurora-time/delete-event-admin-success.png)

---

Trong phần này, bạn đã:

+ Thiết lập **nhóm quyền** trong Cognito (`user`, `admin`).  
+ Kết hợp **Cognito Authorizer + Lambda** để áp dụng phân quyền chi tiết cho API Aurora Time.  
+ Chứng minh được rằng cùng một endpoint nhưng kết quả khác nhau tuỳ theo group của người dùng, tương tự như cách VPC Endpoint Policy giới hạn bucket S3 trong workshop S3/VPC Endpoint.

Cách tiếp cận này giúp Aurora Time tuân theo nguyên tắc **least privilege** và dễ mở rộng khi bạn thêm các vai trò mới (ví dụ: `viewer`, `premium`, …) trong tương lai.[web:299][web:304]
