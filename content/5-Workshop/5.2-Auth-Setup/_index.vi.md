---
title: "Cấu hình Google Cloud & Amazon Cognito"
date: 2025-12-09
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

{{% notice info %}}
⚙️ **Mục tiêu:** Thiết lập dự án trên Google Cloud Platform để lấy OAuth Credentials và cấu hình Amazon Cognito User Pool làm nơi quản lý định danh tập trung.
{{% /notice %}}

# 1. Cấu hình Google Cloud Platform (GCP)

Để cho phép người dùng đăng nhập bằng Gmail, trước tiên chúng ta cần tạo một dự án trên Google Cloud và xin cấp quyền OAuth 2.0.

### Bước 1: Tạo OAuth Client ID
Tiếp theo, vào mục **Credentials** > **Create Credentials** > **OAuth client ID**.
- **Application type:** Web application.
- **Authorized redirect URIs:** Đây là địa chỉ mà Google sẽ trả token về sau khi đăng nhập thành công. (Địa chỉ này sẽ được lấy từ Amazon Cognito Domain ở bước sau).

> **Hình ảnh thực hiện:**
>
> ![Screenshot: Màn hình tạo Client ID và Secret](images/gcp-credentials.png)
> *Hình 5.2.2: Tạo OAuth Client ID và Client Secret.*

{{% notice warning %}}
Lưu ý: Cần copy lại **Client ID** và **Client Secret** để sử dụng cho cấu hình Cognito.
{{% /notice %}}

---

# 2. Cấu hình Amazon Cognito User Pool

Sau khi có thông tin từ Google, chúng ta chuyển sang AWS Console để thiết lập User Pool.

### Bước 1: Tạo User Pool và Identity Provider
Trong giao diện Amazon Cognito, tạo một User Pool mới. Tại phần **Sign-in experience**, chọn **Federated identity providers** và chọn **Google**.

Chúng ta điền **Client ID** và **Client Secret** đã lấy từ bước trên vào đây.

> **Hình ảnh thực hiện:**
>
> ![Screenshot: Cấu hình Google Identity Provider trong Cognito](images/cognito-idp-google.png)
> *Hình 5.2.3: Nhập thông tin xác thực Google vào Cognito.*


### Bước 2: Cấu hình App Client & Domain
Cuối cùng, tại phần **App integration**:
1.  **Domain:** Tạo một Cognito Domain. Domain này dùng để điền ngược lại vào phần *Authorized redirect URIs* bên Google Cloud.
2.  **App Client Settings:**
    - **Allowed callback URLs:** Đường dẫn Frontend của ứng dụng .
    - **OAuth 2.0 Grant Types:** Chọn `Authorization code grant`.
    - **OpenID Connect scopes:** Chọn `email`, `openid`, `profile`.

> **Hình ảnh thực hiện:**
>
> ![Screenshot: Cấu hình App Client Settings](images/cognito-app-client.png)
> *Hình 5.2.5: Cấu hình Redirect URL và OAuth Scopes.*

---

# 3. Kết quả kiểm thử (Hosted UI)

Để kiểm tra cấu hình đã chính xác chưa, chúng ta có thể mở giao diện **Hosted UI** do Cognito cung cấp. Nếu nút "Continue with Google" xuất hiện và hoạt động, cấu hình đã thành công.

> **Hình ảnh thực hiện:**
>
> ![Screenshot: Giao diện đăng nhập có nút Google](images/hosted-ui-login.png)
> *Hình 5.2.6: Giao diện đăng nhập tích hợp Google thành công.*