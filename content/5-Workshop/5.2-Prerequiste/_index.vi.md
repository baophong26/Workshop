---
title: "Các bước chuẩn bị"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

#### Yêu cầu trước khi bắt đầu

Để hoàn thành workshop này, bạn cần:

1. **Tài khoản AWS** với quyền Administrator hoặc đủ quyền tạo các dịch vụ sau:
   - IAM, S3, DynamoDB, Cognito, SQS, Lambda, API Gateway, WAF, CloudFront, Route 53, ACM, CloudWatch, SNS

2. **OpenAI API Key**: Đăng ký tại [platform.openai.com](https://platform.openai.com/) để sử dụng Speech-to-Text và GPT evaluation

3. **Region**: Workshop này sử dụng **ap-southeast-1 (Singapore)** cho hầu hết dịch vụ
   - **Đặc biệt**: ACM SSL Certificate phải tạo ở **us-east-1** để dùng với CloudFront

4. **Email nhận cảnh báo**: Để nhận thông báo từ SNS

5. **(Tùy chọn) Domain riêng**: Nếu muốn dùng tên miền như `itcoach24h.xyz` thay vì CloudFront domain mặc định
   - Có thể mua domain tại Namecheap, GoDaddy, hoặc Route 53 (~$2-3/năm)

#### Checklist tiến độ

Trong workshop này, bạn sẽ tạo các tài nguyên sau:

| # | Dịch vụ | Chi tiết | Trạng thái |
|---|---------|----------|-----------|
| 1 | IAM Role | `itcoach-lambda-role` | ⬜ |
| 2 | S3 - Static Assets | `itcoach-static-assets` | ⬜ |
| 3 | S3 - Audio Upload | `itcoach-audio-upload` | ⬜ |
| 4 | DynamoDB | 8 bảng | ⬜ |
| 5 | Cognito | User Pool + App Client | ⬜ |
| 6 | SQS | 2 queues (Main + DLQ) | ⬜ |
| 7 | Lambda | 8 functions | ⬜ |
| 8 | API Gateway | 8 endpoints + Throttling | ⬜ |
| 9 | AWS WAF | 2 Web ACLs (CloudFront + API Gateway) | ⬜ |
| 10 | CloudFront | Distribution + Error Pages | ⬜ |
| 11 | Route 53 | DNS + Domain `itcoach24h.xyz` | ⬜ |
| 12 | ACM | SSL Certificate | ⬜ |
| 13 | SNS + CloudWatch | Monitoring + Alerts | ⬜ |

#### Thông tin quan trọng cần lưu

Trong quá trình làm workshop, bạn sẽ cần lưu lại các thông tin sau để sử dụng ở các bước tiếp theo:

| Thông tin | Sẽ được tạo ở bước | Dùng cho |
|-----------|-------------------|----------|
| **IAM Role ARN** | 5.3 - IAM Role | Lambda functions |
| **S3 Static Bucket Name** | 5.4 - S3 Buckets | CloudFront origin |
| **S3 Audio Bucket Name** | 5.4 - S3 Buckets | Lambda env vars |
| **DynamoDB Table Names** | 5.5 - DynamoDB | Lambda env vars (8 tables) |
| **Cognito User Pool ID** | 5.6 - Cognito | API Gateway authorizer |
| **Cognito App Client ID** | 5.6 - Cognito | Frontend config |
| **SQS Queue URL** | 5.7 - SQS | Lambda env vars |
| **Lambda Function ARNs** | 5.8 - Lambda | API Gateway integration |
| **API Gateway URL** | 5.9 - API Gateway | Frontend config |
| **CloudFront Domain** | 5.10 - CloudFront | Cognito callback URL |
| **ACM Certificate ARN** | 5.11 - Route 53 | CloudFront SSL |
| **Route 53 Hosted Zone** | 5.11 - Route 53 | DNS management |


#### Ước tính chi phí

Với mức sử dụng thử nghiệm (< 1000 requests/tháng), chi phí ước tính:

| Dịch vụ | Chi phí/tháng | Ghi chú |
|---------|--------------|---------|
| AWS Lambda | ~$0.00 | Free tier: 1M requests |
| DynamoDB | ~$0.00 | Free tier: 25GB |
| S3 | ~$0.05 | Static + audio files |
| API Gateway | ~$0.01 | ~1,000 requests |
| CloudFront | $0.00 | Free tier |
| AWS WAF – CloudFront | $0.00 | Nằm trong 5 rule miễn phí kèm CloudFront Free plan |
| AWS WAF – API Gateway | ~$10–15 | Web ACL Regional, không nằm trong gói miễn phí nào |
| Cognito | $0.00 | Free tier: 50,000 MAU |
| SQS | ~$0.00 | Free tier: 1M requests |
| Polly | ~$0.04 | ~100,000 characters |
| CloudWatch | ~$1–5 | Logs + Alarms |
| SNS | ~$0.00 | Free tier |
| Route 53 | ~$0.50 | Hosted Zone $0.50/tháng |
| ACM | $0.00 | Miễn phí hoàn toàn |
| **Tổng AWS** | **~$12–20/tháng** | |
| **OpenAI API** | ~$1–$5 | Tùy số lượng đánh giá |
| **Tổng với OpenAI** | **~$13–25/tháng** | |

**Chi phí một lần:**
- Domain `itcoach24h.xyz`: ~$2-3/năm (nếu mua domain riêng)


#### Sẵn sàng bắt đầu

Sau khi đã chuẩn bị đầy đủ, hãy chuyển sang bước tiếp theo để bắt đầu tạo IAM Role.

