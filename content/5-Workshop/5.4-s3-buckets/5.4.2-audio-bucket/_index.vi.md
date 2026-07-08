---
title: "Tạo S3 Bucket cho Audio Upload"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

#### Mục đích

Bucket này sẽ lưu trữ:
- File ghi âm từ người dùng (upload qua Presigned URL)
- File audio feedback từ Amazon Polly

Bucket này sẽ được giữ **private** và chỉ Lambda có quyền truy cập.

#### Các bước thực hiện

**1. Tạo Bucket mới**

- Ở S3 Console, click **Create bucket**

**2. Cấu hình Bucket**

**General configuration:**
- Bucket name: `itcoach-audio-upload`
- AWS Region: `ap-southeast-1` (Singapore)

**Block Public Access settings:**
- **GIỮ NGUYÊN** "Block all public access" được tick
- Bucket này phải private để bảo mật file audio

![Private Bucket](/images/5-Workshop/5.4-s3-buckets/003-audio-bucket-private.png)

**Các setting khác:**
- Giữ mặc định tất cả
- Click **Create bucket**

**3. Cấu hình CORS**

Sau khi bucket được tạo:

- Click vào bucket name `itcoach-audio-upload`
- Chọn tab **Permissions**
- Kéo xuống mục **Cross-origin resource sharing (CORS)**
- Click **Edit**

Dán nội dung JSON sau:

```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["GET", "PUT", "POST", "DELETE"],
    "AllowedOrigins": ["*"],
    "ExposeHeaders": ["ETag"]
  }
]
```

![CORS Config](/images/5-Workshop/5.4-s3-buckets/004-cors-config.png)

- Click **Save changes**


#### Kết quả

✅ Bucket `itcoach-audio-upload` đã được tạo với CORS configuration

#### Thông tin cần lưu

```
Bucket Name: itcoach-audio-upload
Region: ap-southeast-1
Access: Private (Block public access enabled)
CORS: Configured for direct browser upload
```

#### Giải thích về Presigned URL

Lambda function sẽ tạo **Presigned URL** - một URL tạm thời cho phép upload file lên S3 bucket private này mà không cần credentials. URL này:
- Có thời gian hết hạn (ví dụ: 5 phút)
- Chỉ có quyền PUT cho 1 object cụ thể
- An toàn hơn việc cho phép public upload

#### Tiếp theo

Chuyển sang bước tiếp theo để tạo DynamoDB Tables.

