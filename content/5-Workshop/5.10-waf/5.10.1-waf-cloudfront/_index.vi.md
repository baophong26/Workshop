---
title: "WAF cho CloudFront"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.10.1. </b> "
---

#### WAF cho CloudFront (Global Scope)

WAF cho CloudFront bảo vệ frontend React + TypeScript khỏi các cuộc tấn công như SQL Injection, XSS, và DDoS.

#### Đặc điểm WAF CloudFront

- **Scope**: Global (us-east-1)
- **Tự động tạo**: CloudFront có thể tự động tạo Web ACL khi enable WAF
- **Rules**: 3 managed rules + 1 rate-limit rule
- **Chi phí**: Miễn phí trong Free Tier (tối đa 5 rules)

#### Các bước thực hiện

**1. Truy cập CloudFront Console**

- Tìm kiếm **CloudFront**
- Click vào Distribution đã tạo trước đó

**2. Enable WAF cho CloudFront**

- Tab **Security** → **AWS WAF**
- Click **Enable AWS WAF**
- Chọn **Create new Web ACL**

**3. Cấu hình Web ACL**

**Web ACL Details:**
- Name: `itcoach-cloudfront-waf`
- Resource type: **CloudFront distributions**
- Region: **Global (CloudFront)**

**4. Thêm Managed Rules**

Click **Add rules** → **Add managed rule groups**

Chọn 3 managed rules sau:

**a) AWS Managed Rules - Core rule set**
- Name: `AWSManagedRulesCommonRuleSet`
- Bảo vệ: SQL Injection, XSS, Path Traversal
- Priority: 10

**b) AWS Managed Rules - Known bad inputs**
- Name: `AWSManagedRulesKnownBadInputsRuleSet`
- Bảo vệ: Known malicious patterns
- Priority: 20

**c) AWS Managed Rules - Amazon IP reputation list**
- Name: `AWSManagedRulesAmazonIpReputationList`
- Bảo vệ: Chặn IP xấu từ danh sách Amazon
- Priority: 30

**5. Thêm Rate Limit Rule**

Click **Add rules** → **Add my own rules and rule groups** → **Rule builder**

**Rate Limit Rule:**
- Name: `RateLimitRule`
- Type: **Rate-based rule**
- Rate limit: **2000 requests per 5 minutes per IP**
- Action: **Block**
- Priority: 40

**6. Default Action**

- Default action: **Allow**
- Chỉ block requests vi phạm rules

**7. Review và Create**

- Review lại cấu hình
- Click **Create Web ACL**

**8. Associate với CloudFront**

Web ACL sẽ tự động associate với CloudFront distribution. Kiểm tra:

- Tab **Associated AWS resources**
- CloudFront distribution phải xuất hiện trong danh sách

#### Kết quả

✅ WAF cho CloudFront đã sẵn sàng bảo vệ frontend

#### Thông tin cần lưu

```
Web ACL Name: itcoach-cloudfront-waf
Scope: Global (CloudFront)
Region: us-east-1
Rules:
  - AWSManagedRulesCommonRuleSet (Priority 10)
  - AWSManagedRulesKnownBadInputsRuleSet (Priority 20)
  - AWSManagedRulesAmazonIpReputationList (Priority 30)
  - RateLimitRule: 2000 req/5min (Priority 40)
Default Action: Allow
```

#### Test WAF CloudFront

Truy cập CloudFront domain nhiều lần liên tiếp để test rate limit:

```bash
for i in {1..2100}; do curl -I https://xxxxxxxxxxxx.cloudfront.net; done
```

Sau 2000 requests trong 5 phút, IP sẽ bị block tạm thời.

#### CloudWatch Metrics

Xem metrics WAF tại:

- CloudWatch → Metrics → **WAF**
- Filter: `itcoach-cloudfront-waf`
- Metrics: AllowedRequests, BlockedRequests, CountedRequests

#### Tiếp theo

Chuyển sang bước tiếp theo để thiết lập WAF cho API Gateway (Regional scope).
