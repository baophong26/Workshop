---
title: "Deploy Code"
date: 2024-01-01
weight: 14
chapter: false
pre: " <b> 5.14. </b> "
---

#### Giới thiệu

Sau khi đã thiết lập xong toàn bộ hạ tầng AWS, bước tiếp theo là deploy code thực tế để hệ thống hoạt động. Phần này hướng dẫn cách deploy Frontend (React + TypeScript) và Backend (Lambda functions).

---

## 1. Deploy Frontend (React + TypeScript)

### Bước 1: Build Frontend

Trên máy local, chạy lệnh build:

```bash
npm run build
```

Sau khi build xong, bạn sẽ có thư mục `/dist` hoặc `/build` chứa các file HTML, CSS, JS đã được optimize.

### Bước 2: Upload lên S3

1. Vào **S3** → Buckets → chọn `itcoach-static-assets`
2. Click **Upload**
3. Kéo thả **toàn bộ nội dung** trong thư mục `/dist` (không kéo thư mục /dist, mà kéo files bên trong)
4. Click **Upload**

### Bước 3: Invalidate CloudFront Cache

Để người dùng thấy được version mới nhất, bạn cần xóa cache CloudFront:

1. Vào **CloudFront** → Distributions
2. Chọn `itcoach-distribution`
3. Tab **Invalidations** → **Create invalidation**
4. Object paths: `/*`
5. **Create invalidation**

Quá trình invalidation mất khoảng 1-3 phút.

### Bước 4: Kiểm tra

Truy cập `https://itcoach24h.xyz` (hoặc CloudFront domain) để kiểm tra frontend đã hiển thị đúng chưa.

---

## 2. Deploy Backend (Lambda Functions)

### Bước 1: Đóng gói Lambda Functions

Mỗi Lambda function cần được đóng gói thành file `.zip` bao gồm:
- Code Python
- Dependencies (thư viện bên thứ 3)

Ví dụ cấu trúc:
```
itcoach-auth-handler.zip
├── lambda_function.py
└── (các thư viện nếu có)
```

### Bước 2: Upload Code lên Lambda

Làm lần lượt cho 8 functions:

1. Vào **Lambda** → Functions
2. Chọn function (ví dụ: `itcoach-auth-handler`)
3. Tab **Code** → **Upload from** → **.zip file**
4. Chọn file `.zip` tương ứng
5. **Save**
6. Chờ Lambda deploy xong (màn hình hiện "Successfully updated")

### Bước 3: Test Lambda

1. Tab **Test** → **Create test event**
2. Event name: `test-event`
3. Dán JSON test event mẫu
4. **Save** → **Test**
5. Kiểm tra **Execution result** có trả về đúng không

---

## 3. Kiểm Tra Tổng Thể

### Test API Endpoints

Dùng Postman hoặc curl để test:

```bash
# Test public endpoint
curl -X POST https://your-api-url/prod/auth \
  -H "Content-Type: application/json" \
  -d '{"action":"register","email":"test@example.com"}'

# Test protected endpoint (cần token)
curl -X GET https://your-api-url/prod/questions \
  -H "Authorization: Bearer YOUR_COGNITO_TOKEN"
```

### Test Frontend

1. Mở `https://itcoach24h.xyz`
2. Đăng ký tài khoản mới
3. Đăng nhập
4. Thử các tính năng:
   - Quiz trắc nghiệm
   - Tự luận ghi âm
   - Dashboard
   - Leaderboard

---

## 4. Monitoring sau Deploy

### Kiểm tra CloudWatch Logs

1. **CloudWatch** → Log groups
2. Tìm `/aws/lambda/itcoach-*`
3. Xem logs của các Lambda functions
4. Kiểm tra có lỗi không

### Kiểm tra CloudWatch Alarms

Nếu đã tạo alarms ở section 5.12:
- Alarms sẽ chuyển từ "Insufficient data" sang "OK" sau khi có traffic thật
- Nếu có lỗi, alarms sẽ chuyển sang "In alarm" và gửi email qua SNS

---

## 5. Cập Nhật Cognito Callback URL

Sau khi có domain thật, cập nhật lại Cognito:

1. **Cognito** → User pools → chọn pool
2. Tab **App integration** → chọn App client
3. **Edit Hosted UI settings**
4. Allowed callback URLs:
   - Thêm: `https://itcoach24h.xyz/callback`
   - Xóa: `http://localhost:3000` (nếu không cần nữa)
5. **Save changes**

---

## Kết quả

- Frontend đã deploy và hiển thị trên domain
- Backend Lambda functions đã có code thật
- API endpoints hoạt động đúng
- Monitoring đang theo dõi hệ thống

**Hệ thống ITCoach đã sẵn sàng vận hành!**

#### Bước tiếp theo

Chuyển sang [Dọn dẹp tài nguyên](../5.14-cleanup/) nếu bạn muốn xóa toàn bộ hệ thống.
