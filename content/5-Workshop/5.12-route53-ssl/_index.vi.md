---
title: "Cấu hình Route 53 và SSL"
date: 2024-01-01
weight: 12
chapter: false
pre: " <b> 5.12. </b> "
---

#### Giới thiệu

Phần này hướng dẫn cấu hình custom domain với HTTPS cho ITCoach. Bạn sẽ:
- Mua domain (ví dụ: itcoach24h.xyz)
- Tạo SSL certificate với ACM
- Cấu hình Route 53 DNS
- Gắn domain vào CloudFront


#### Bước 1: Mua Domain (Namecheap)

**1. Truy cập Namecheap.com**
- Tìm domain muốn mua (ví dụ: `itcoach24h.xyz`)
- Add to cart

**2. Checkout**
- Tắt "I'm registering on behalf of a company"
- Giữ **Free Domain Privacy** ✅
- Bỏ tick **Auto-renew** (để tránh tự động gia hạn)
- Thanh toán bằng thẻ quốc tế

#### Bước 2: Tạo Hosted Zone trên Route 53

**1. Tạo Hosted Zone**
- Tìm kiếm **Route 53** → **Hosted zones** → **Create hosted zone**
- Domain name: `itcoach24h.xyz`
- Type: **Public hosted zone**
- **Create hosted zone**

![Create Hosted Zone](/images/5-Workshop/5.12-route53/001-route53-hosted-zone.png)

**2. Lấy NS Records**
- Sau khi tạo, bạn sẽ thấy 4 dòng **NS records**
- Copy 4 nameservers (dạng `ns-xxx.awsdns-xx.com`)

**3. Cập nhật Nameservers trên Namecheap**
- Vào Namecheap → Dashboard → quản lý domain
- **Nameservers** → chọn **Custom DNS**
- Dán 4 nameservers từ Route 53
- **Save**

![Update Nameservers](/images/5-Workshop/5.12-route53/002-namecheap-custom-dns.png)


#### Bước 3: Xin SSL Certificate (ACM)


**1. Đổi Region**
- Góc trên phải AWS Console → đổi region sang **us-east-1**

**2. Request Certificate**
- Tìm kiếm **Certificate Manager (ACM)**
- **Request a certificate** → **Next**

**3. Cấu hình Certificate**
- Fully qualified domain name:
  - Domain 1: `itcoach24h.xyz`
  - Click **Add another name** → Domain 2: `*.itcoach24h.xyz`
- Validation method: **DNS validation**
- **Request**

![Request Certificate](/images/5-Workshop/5.12-route53/003-acm-request-cert.png)

**4. Validate Certificate**
- Click vào certificate (status *Pending validation*)
- Tab **Domains** → **Create records in Route 53**
- **Create records**

Chờ 3-5 phút → Status chuyển **Issued** (xanh) ✅

#### Bước 4: Gắn Domain vào CloudFront


**1. Edit CloudFront Distribution**
- **CloudFront** → click distribution `itcoach-distribution`
- Tab **General** → **Edit**

**2. Thêm Alternate Domain Names**
- **Alternate domain names (CNAMEs)** → **Add item**
  - Thêm: `itcoach24h.xyz`
  - Thêm: `www.itcoach24h.xyz`

**3. Chọn SSL Certificate**
- **Custom SSL certificate** → chọn certificate vừa tạo
- **Save changes**

![CloudFront Custom Domain](/images/5-Workshop/5.12-route53/004-cloudfront-custom-domain.png)

#### Bước 5: Tạo DNS Records

**1. Tạo A Record cho Root Domain**
- **Route 53** → **Hosted zones** → click `itcoach24h.xyz`
- **Create record**
  - Record name: *(để trống)*
  - Record type: **A**
  - Bật toggle **Alias** ✅
  - Route traffic to: **Alias to CloudFront distribution**
  - Chọn distribution của bạn
  - **Create records**

**2. Tạo A Record cho www**
- **Create record**
  - Record name: `www`
  - Record type: **A**
  - Bật toggle **Alias** ✅
  - Route traffic to: **Alias to CloudFront distribution**
  - Chọn distribution của bạn
  - **Create records**

![DNS Records](/images/5-Workshop/5.12-route53/005-route53-alias-record.png)

#### Bước 6: Test Domain

Truy cập domain trên browser:
```
https://itcoach24h.xyz
https://www.itcoach24h.xyz
```

Kiểm tra SSL certificate bằng cách click vào icon khóa trên thanh địa chỉ.

#### Kết quả

✅ Custom domain với HTTPS đã hoạt động!

#### Thông tin cần lưu

```
Domain: itcoach24h.xyz
SSL Certificate: ACM us-east-1 (Issued)
Nameservers: AWS Route 53
CloudFront CNAMEs: itcoach24h.xyz, www.itcoach24h.xyz
DNS Records: A records (Alias to CloudFront)
```

#### Chi phí ước tính

- Domain .xyz: ~$1-2/năm (Namecheap)
- Route 53 Hosted Zone: $0.50/tháng
- ACM Certificate: **FREE**
- DNS Queries: $0.40/triệu queries

**Tổng: ~$0.50/tháng + $2/năm domain**

#### Tiếp theo

Chuyển sang bước tiếp theo để thiết lập Monitoring với CloudWatch.

