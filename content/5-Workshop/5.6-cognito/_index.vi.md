---
title: "Cấu hình Amazon Cognito"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

#### Giới thiệu về Amazon Cognito

Amazon Cognito cung cấp xác thực, ủy quyền và quản lý người dùng cho ứng dụng web và mobile. Trong ITCoach, Cognito sẽ:
- Quản lý đăng ký/đăng nhập người dùng
- Tạo JWT tokens cho authentication
- Bảo vệ API Gateway endpoints

#### Các bước thực hiện

**1. Truy cập Cognito Console**

- Tìm kiếm **Cognito** trong thanh tìm kiếm AWS Console
- Click vào **Amazon Cognito**

**2. Tạo User Pool**

- Click nút **Create user pool**

![Cognito Config](/images/5-Workshop/5.6-cognito/001-cognito-config.png)


**3. Cấu hình User Pool trên 1 trang**

**Application type:**
- Chọn **Single-page application (SPA)**

**Name your application:**
- Application name: `itcoach-web-client`

**Sign-in options:**
- Tick ✅ **Email**
- Bỏ tick Username và Phone number

**Self-registration:**
- ✅ **Enable self-registration** (giữ nguyên - cho phép user tự đăng ký)

**Required attributes:**
- Click **Select attributes**
- Tick thêm: **name** (Họ tên người dùng)
- Email đã được chọn tự động

**Password policy:**
- Giữ mặc định (Cognito defaults)

**Multi-factor authentication (MFA):**
- Chọn **No MFA** (để đơn giản cho workshop)

**Return URL:**
- Nhập: `http://localhost:3000`
- (Sau này sẽ update thành CloudFront URL)

**Email provider:**
- Giữ mặc định: **Send email with Amazon SES**

- Click nút **Create user directory** (nút cam)

**4. Chờ tạo User Pool**

Quá trình tạo mất khoảng 10-20 giây.

**5. Lưu thông tin User Pool ID**

- Sau khi tạo xong, bạn sẽ thấy **User pool ID** (dạng: `ap-southeast-1_xxxxxxxx`)
- Copy và lưu lại

![User Pool ID](/images/5-Workshop/5.6-cognito/002-user-pool-id.png)

**6. Lưu thông tin App Client ID**

- Click vào tab **App clients** (hoặc **App integration**)
- Tìm client `itcoach-web-client`
- Copy **Client ID** (dạng: chuỗi 26 ký tự)

![App Client ID](/images/5-Workshop/5.6-cognito/003-app-client-id.png)

#### Kết quả

✅ Amazon Cognito User Pool đã được cấu hình thành công

#### Thông tin cần lưu

```
User Pool ID: ap-southeast-1_xxxxxxxx
App Client ID: xxxxxxxxxxxxxxxxxxxxxxxxxxxx
Region: ap-southeast-1
Application Name: itcoach-web-client
Sign-in: Email
Return URL: http://localhost:3000 (tạm thời)
```


#### Cách hoạt động

1. **User đăng ký**: Frontend gọi Cognito API → Cognito gửi email xác nhận
2. **User đăng nhập**: Cognito trả về **JWT token** (ID token, Access token)
3. **User gọi API**: Frontend gửi token trong header `Authorization: Bearer <token>`
4. **API Gateway**: Xác thực token với Cognito trước khi cho qua Lambda

#### Tiếp theo

Chuyển sang bước tiếp theo để tạo Amazon SQS.

