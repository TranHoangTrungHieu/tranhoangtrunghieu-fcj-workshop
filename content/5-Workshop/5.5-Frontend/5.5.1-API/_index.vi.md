---
title: "Tạo API Gateway & Authen"
date: 2025-12-09
weight: 1
chapter: false
pre: " <b> 5.6.1. </b> "
---

{{% notice tip %}}
🛡️ **Mục tiêu:** Tạo HTTP API để gom các hàm Lambda lại thành một endpoint duy nhất và bảo vệ chúng bằng Cognito Authorizer.
{{% /notice %}}

# Bước 1: Tạo HTTP API

1. Truy cập **AWS Console** > **API Gateway**.
2. Chọn **HTTP API** (chi phí thấp, hiệu năng cao) > Bấm **Build**.
3. **API name:** `AuroraAPI`.
4. Bấm **Next** và để trống các phần Integrations (sẽ thêm sau).
5. **Stage:** Để mặc định `$default` (Auto-deploy). Bấm **Create**.

> **Hình ảnh:**
> ![Screenshot: Tạo HTTP API Gateway](images/api-create.png)

# Bước 2: Kết nối Lambda (Integrations)

Chúng ta cần khai báo API này sẽ trỏ đến các hàm Lambda nào (đã tạo ở phần 5.4).

1. Vào menu **Integrations** > **Manage integrations** > **Create**.
2. Chọn **Lambda function**.
3. Chọn hàm `auroratimeEvent` (hoặc các hàm bạn đã tạo).
4. Làm tương tự cho các hàm khác (`auroratimeTodo`, v.v...).

> **Hình ảnh:**
> ![Screenshot: Tạo Integration trỏ vào Lambda](images/api-integration.png)

# Bước 3: Tạo Routes (Đường dẫn)

1. Vào menu **Routes** > **Create**.
2. Định nghĩa các đường dẫn API:
    * `POST /events` -> Chọn integration `auroratimeEvent`
    * `GET /events` -> Chọn integration `auroratimeEvent`
    * `POST /todos` -> Chọn integration `auroratimeTodo`
    * ...
    *(Lưu ý: Logic phân chia action nằm trong code Lambda hoặc chia route chi tiết hơn tùy bạn)*

> **Hình ảnh:**
> ![Screenshot: Danh sách Routes API](images/api-routes.png)

# Bước 4: Cấu hình CORS (Quan trọng)

Để Frontend (Amplify) gọi được API, phải mở CORS.
1. Vào menu **CORS**.
2. **Access-Control-Allow-Origin:** `*` .
3. **Access-Control-Allow-Methods:** `GET, POST, PUT, DELETE, OPTIONS`.
4. **Access-Control-Allow-Headers:** `Content-Type, Authorization`.
5. Bấm **Save**.

> **Hình ảnh:**
> ![Screenshot: Cấu hình CORS cho API Gateway](images/api-cors.png)

# Bước 5: Cấu hình Authentication (JWT Authorizer)

Đây là bước bảo mật API. Chỉ nhận request có Token từ Cognito.

1. Vào menu **Authorization** > Chọn tab **Manage authorizers** > **Create**.
2. **Authorizer type:** JWT.
3. **Name:** `CognitoAuth`.
4. **Identity source:** `$request.header.Authorization`.
5. **Issuer URL:** `https://cognito-idp.ap-southeast-1.amazonaws.com/ap-southeast-1_TryyHPjm0` (Thay User Pool ID của bạn vào).
6. **Audience:** 5dct7sk93a0unassp7komfpidq
7. Bấm **Create**.
8. **Gán Authorizer:** Quay lại tab **Attach authorizers to routes**, chọn các route (`/events`, `/todos`...) và gán `CognitoAuth` cho chúng.

> **Hình ảnh:**
> ![Screenshot: Gán JWT Authorizer cho Route](images/api-authorizer.png)