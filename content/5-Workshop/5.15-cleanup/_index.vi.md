---
title: "Dọn dẹp tài nguyên"
date: 2024-01-01
weight: 15
chapter: false
pre: " <b> 5.15. </b> "
---

#### Tại sao cần dọn dẹp?

Sau khi hoàn thành workshop, bạn nên dọn dẹp tài nguyên để:
- Tránh phí không mong muốn
- Giữ AWS account sạch sẽ
- Học cách quản lý lifecycle resources


#### Thứ tự dọn dẹp

### 1. Xóa CloudFront Distribution

- CloudFront → Distributions
- Chọn `itcoach-distribution`
- **Disable** distribution trước (chờ 5-10 phút)
- Sau khi disabled → **Delete**


### 2. Xóa AWS WAF Web ACLs (2 Web ACLs)

**⚠️ Quan trọng:** Phải xóa WAF **sau khi** disable CloudFront và trước khi xóa API Gateway

**2.1. Xóa WAF CloudFront (us-east-1):**
- Đổi region sang **us-east-1**
- WAF & Shield → Web ACLs
- Chọn `itcoach-cloudfront-waf`
- **Delete**

**2.2. Xóa WAF API Gateway (ap-southeast-1):**
- Đổi region sang **ap-southeast-1**
- WAF & Shield → Web ACLs
- Chọn `itcoach-api-waf`
- **Delete**


### 3. Xóa API Gateway

- API Gateway → APIs
- Chọn `itcoach-api`
### 3. Xóa API Gateway

- API Gateway → APIs
- Chọn `itcoach-api`
- **Actions** → **Delete API**
- Xác nhận xóa


### 4. Xóa Lambda Functions (8 functions)

- Lambda → Functions
- Chọn từng function → **Actions** → **Delete**
- Lặp lại cho 8 functions


### 5. Xóa SQS Queues (2 queues)

- SQS → Queues
- Chọn `itcoach-processing-queue` → **Delete**
- Chọn `itcoach-dlq` → **Delete**


### 6. Xóa Cognito User Pool

- Cognito → User pools
- Chọn user pool → **Delete**
- Nhập tên pool để xác nhận


### 7. Xóa DynamoDB Tables (8 tables)

- DynamoDB → Tables
- Chọn từng table → **Delete**
- Lặp lại cho 8 tables



### 8. Xóa S3 Buckets (2 buckets)

**Quan trọng:** Phải **empty bucket trước** khi xóa

- S3 → Buckets
- Chọn `itcoach-static-assets`
- **Empty** bucket (xóa tất cả objects)
- Sau khi empty → **Delete** bucket
- Lặp lại cho `itcoach-audio-upload`



### 9. Xóa IAM Role

- IAM → Roles
- Tìm `itcoach-lambda-role`
- **Delete** role


### 10. Xóa SNS Topic và Subscription

- SNS → Topics
- Chọn `itcoach-alerts` → **Delete**
- Subscriptions sẽ tự động bị xóa


### 11. Xóa CloudWatch Alarms (nếu đã tạo)

- CloudWatch → Alarms
- Chọn tất cả alarms liên quan → **Delete**

#### Checklist Cleanup

| # | Resource | Status |
|---|----------|--------|
| 1 | CloudFront Distribution | ⬜ |
| 2 | AWS WAF Web ACLs (2) | ⬜ |
| 3 | API Gateway | ⬜ |
| 4 | Lambda Functions (8) | ⬜ |
| 5 | SQS Queues (2) | ⬜ |
| 6 | Cognito User Pool | ⬜ |
| 7 | DynamoDB Tables (8) | ⬜ |
| 8 | S3 Buckets (2) | ⬜ |
| 9 | IAM Role | ⬜ |
| 10 | SNS Topic | ⬜ |
| 11 | CloudWatch Alarms | ⬜ |

#### Xác nhận đã dọn dẹp xong

Kiểm tra lại từng service để đảm bảo không còn resources:

```
✅ CloudFront: 0 distributions
✅ WAF: 0 Web ACLs
✅ API Gateway: 0 APIs
✅ Lambda: 0 functions (trừ functions khác của bạn)
✅ SQS: 0 queues liên quan
✅ Cognito: 0 user pools liên quan
✅ DynamoDB: 0 tables liên quan
✅ S3: 0 buckets liên quan
✅ IAM: Role itcoach-lambda-role đã xóa
✅ SNS: Topic itcoach-alerts đã xóa
```

#### Kết luận

Chúc mừng! Bạn đã hoàn thành workshop ITCoach trên AWS Serverless! 🎉

Những gì bạn đã học:
- ✅ Thiết lập IAM roles và permissions
- ✅ Cấu hình S3 cho static hosting và private storage
- ✅ Tạo và quản lý 8 bảng DynamoDB
- ✅ Xác thực người dùng với Cognito
- ✅ Xử lý bất đồng bộ với SQS
- ✅ Xây dựng 8 Lambda functions serverless
- ✅ Tạo REST API với API Gateway
- ✅ Phân phối CDN toàn cầu với CloudFront
- ✅ Monitoring với CloudWatch và SNS
- ✅ Clean up resources đúng cách

**Kiến thức này có thể áp dụng cho nhiều dự án Serverless khác!**

