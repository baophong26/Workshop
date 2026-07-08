---
title: "Tạo S3 Bucket cho Static Assets"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

#### Mục đích

Bucket này sẽ lưu trữ frontend React + TypeScript đã build (HTML, CSS, JavaScript) và được cấu hình làm Static Website Hosting để CloudFront phân phối.

#### Các bước thực hiện

**1. Truy cập S3 Console**

- Tìm kiếm **S3** trong thanh tìm kiếm AWS Console
- Click vào **S3** để mở S3 Dashboard

**2. Tạo Bucket mới**

- Click nút **Create bucket**

**3. Cấu hình Bucket**

**General configuration:**
- Bucket name: `itcoach-static-assets`
- AWS Region: `ap-southeast-1` (Singapore)

**Object Ownership:**
- Giữ mặc định: **ACLs disabled**

**Block Public Access settings:**
- **BỎ TICK** "Block all public access"
- Tick vào ô xác nhận: "I acknowledge that the current settings might result in this bucket and the objects within becoming public"

**Bucket Versioning:**
- Giữ mặc định: **Disable**

**Encryption:**
- Giữ mặc định: **Server-side encryption with Amazon S3 managed keys (SSE-S3)**

![Static Bucket Config](/images/5-Workshop/5.4-s3-buckets/001-static-bucket-config.png)

- Click **Create bucket**

**4. Kích hoạt Static Website Hosting**

Sau khi bucket được tạo:

- Click vào bucket name `itcoach-static-assets`
- Chọn tab **Properties**
- Kéo xuống cuối trang, tìm mục **Static website hosting**
- Click **Edit**

Cấu hình:
- Static website hosting: chọn **Enable**
- Hosting type: **Host a static website**
- Index document: `index.html`
- Error document: `index.html` (cho React Router)

- Click **Save changes**

**5. Lưu Website Endpoint**

Sau khi save, kéo lại xuống mục **Static website hosting**, bạn sẽ thấy **Bucket website endpoint**.

Copy URL này (dạng: `http://itcoach-static-assets.s3-website-ap-southeast-1.amazonaws.com`)

![Website Endpoint](/images/5-Workshop/5.4-s3-buckets/002-website-endpoint.png)

#### Kết quả

✅ Bucket `itcoach-static-assets` đã được tạo và cấu hình Static Website Hosting

#### Thông tin cần lưu

```
Bucket Name: itcoach-static-assets
Region: ap-southeast-1
Website Endpoint: http://itcoach-static-assets.s3-website-ap-southeast-1.amazonaws.com
```


#### Tiếp theo

Chuyển sang bước tiếp theo để tạo S3 Bucket cho Audio Upload.

