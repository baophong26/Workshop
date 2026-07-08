---
title: "Thiết lập CloudFront"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---

#### Giới thiệu về CloudFront

Amazon CloudFront là Content Delivery Network (CDN) phân phối nội dung với độ trễ thấp. Trong ITCoach, CloudFront sẽ:
- Phân phối React + TypeScript frontend toàn cầu
- Cache static assets (HTML, CSS, JS)
- Cung cấp HTTPS
- Handle React Router (SPA routing)

#### Các bước thực hiện

**1. Truy cập CloudFront Console**

- Tìm kiếm **CloudFront**
- Click vào **CloudFront**

**2. Create Distribution**

- Click **Create distribution**

**Origin Settings:**
- Origin domain: Chọn S3 bucket `itcoach-static-assets` hoặc dán S3 website endpoint
- Origin path: *(để trống)*
- Name: `itcoach-s3-origin`

**Default Cache Behavior:**
- Viewer protocol policy: **Redirect HTTP to HTTPS**
- Allowed HTTP methods: **GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE**
- Cache policy: **CachingOptimized**

**Distribution Settings:**
- Price class: **Use all edge locations (best performance)**
- Alternate domain name (CNAME): *(để trống nếu chưa có custom domain)*
- Default root object: `index.html`

![CloudFront Config](/images/5-Workshop/5.10-cloudfront/001-cloudfront-config.png)

- Click **Create distribution**

**3. Chờ CloudFront Deploy**

Quá trình deploy mất **5-15 phút**. Status sẽ chuyển từ **Deploying** → **Deployed**.

**4. Cấu hình Error Pages (React Router)**

Để React Router hoạt động (SPA routing):

- Click vào distribution
- Tab **Error pages** → **Create custom error response**

Tạo 2 error responses:

| HTTP error code | Response page path | HTTP response code |
|----------------|-------------------|-------------------|
| `403` | `/index.html` | `200` |
| `404` | `/index.html` | `200` |

![Error Pages](/images/5-Workshop/5.10-cloudfront/002-domain-error-pages.png)

**5. Lưu CloudFront Domain**

- Copy **Distribution domain name**
- Dạng: `https://xxxxxxxxxxxx.cloudfront.net`

**6. Update Cognito Return URL (QUAN TRỌNG)**

Quay lại Cognito User Pool:

- Tab **App integration** → Edit callback URL
- Thay `http://localhost:3000` thành CloudFront domain
- **Save changes**

#### Kết quả

✅ CloudFront distribution đã sẵn sàng phân phối frontend

#### Thông tin cần lưu

```
Distribution Name: itcoach-distribution
Domain: https://xxxxxxxxxxxx.cloudfront.net
Origin: itcoach-static-assets (S3 website endpoint)
Default Root: index.html
Error Pages: 403→200, 404→200 (React Router)
```

#### Test CloudFront

Truy cập CloudFront domain trên browser:
```
https://xxxxxxxxxxxx.cloudfront.net
```

Hiện tại sẽ báo lỗi vì chưa upload React + TypeScript. Sau khi dev xong frontend và upload lên S3, trang web sẽ hoạt động.

#### Tiếp theo

Chuyển sang bước tiếp theo để thiết lập Monitoring với CloudWatch và SNS.

