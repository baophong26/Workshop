---
title: "WAF cho API Gateway"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.10.2. </b> "
---

#### WAF cho API Gateway (Regional Scope)

WAF cho API Gateway bảo vệ backend API khỏi các cuộc tấn công trực tiếp từ React + TypeScript app. Vì app gọi API Gateway trực tiếp (không qua CloudFront), chúng ta cần WAF riêng cho API Gateway.

#### Đặc điểm WAF API Gateway

- **Scope**: Regional (ap-southeast-1)
- **Tạo thủ công**: Phải tạo Web ACL riêng và associate với API Gateway
- **Rules**: 3 managed rules + 2 rate-limit rules (general + auth endpoint)
- **Chi phí**: ~$5-10/tháng tuỳ traffic

#### Các bước thực hiện

**1. Truy cập WAF Console**

- Tìm kiếm **WAF** hoặc **AWS WAF & Shield**
- Đảm bảo Region: **Asia Pacific (Singapore) - ap-southeast-1**

**2. Create Web ACL**

- Click **Create Web ACL**

**Web ACL Details:**
- Name: `itcoach-api-waf`
- Resource type: **Regional resources**
- Region: **Asia Pacific (Singapore)**

**Associated AWS resources:**
- Click **Add AWS resources**
- Resource type: **API Gateway**
- Chọn API Gateway stage đã tạo trước đó: `itcoach-api/prod`
- Click **Add**

**3. Thêm Managed Rules**

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

**4. Thêm Rate Limit Rule - General**

Click **Add rules** → **Add my own rules and rule groups** → **Rule builder**

**General Rate Limit:**
- Name: `GeneralRateLimitRule`
- Type: **Rate-based rule**
- Rate limit: **2000 requests per 5 minutes per IP**
- Action: **Block**
- Priority: 40

**5. Thêm Rate Limit Rule - Auth Endpoint**

Endpoint `/auth` cần bảo vệ đặc biệt khỏi brute-force attacks.

Click **Add rules** → **Add my own rules and rule groups** → **Rule builder**

**Auth Endpoint Rate Limit:**
- Name: `AuthRateLimitRule`
- Type: **Rate-based rule**
- Rate limit: **20 requests per 5 minutes per IP**

**Scope down statement:**
- Inspect: **URI path**
- Match type: **Starts with string**
- String to match: `/auth`

**Action**: **Block**
**Priority**: 50

Cấu hình này giới hạn mỗi IP chỉ được gọi `/auth` tối đa 20 lần trong 5 phút, ngăn chặn brute-force login.

**6. Default Action**

- Default action: **Allow**
- Chỉ block requests vi phạm rules

**7. CloudWatch Metrics**

- Enable: **Amazon CloudWatch metrics**
- Metric name: `itcoach-api-waf`

**8. Review và Create**

- Review lại cấu hình
- Click **Create Web ACL**

**9. Kiểm tra Association**

Quay lại API Gateway Console:

- API Gateway → Stages → **prod**
- Tab **Web ACL**
- Phải thấy: `itcoach-api-waf`

#### Kết quả

✅ WAF cho API Gateway đã sẵn sàng bảo vệ backend API

#### Thông tin cần lưu

```
Web ACL Name: itcoach-api-waf
Scope: Regional
Region: ap-southeast-1
Associated Resource: itcoach-api (stage: prod)
Rules:
  - AWSManagedRulesCommonRuleSet (Priority 10)
  - AWSManagedRulesKnownBadInputsRuleSet (Priority 20)
  - AWSManagedRulesAmazonIpReputationList (Priority 30)
  - GeneralRateLimitRule: 2000 req/5min (Priority 40)
  - AuthRateLimitRule: 20 req/5min for /auth (Priority 50)
Default Action: Allow
```

#### Test WAF API Gateway

**Test General Rate Limit:**

```bash
for i in {1..2100}; do curl -I https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod/questions; done
```

**Test Auth Rate Limit (nghiêm ngặt hơn):**

```bash
for i in {1..25}; do curl -I https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod/auth; done
```

Sau 20 requests đến `/auth` trong 5 phút, IP sẽ bị block.

#### CloudWatch Metrics

Xem metrics WAF tại:

- CloudWatch → Metrics → **WAFV2**
- Region: **ap-southeast-1**
- Filter: `itcoach-api-waf`
- Metrics: AllowedRequests, BlockedRequests

#### CloudWatch Alarms (Optional)

Tạo alarm khi số request bị block tăng cao:

- CloudWatch → Alarms → **Create alarm**
- Metric: `WAFV2 > itcoach-api-waf > BlockedRequests`
- Condition: `>= 100` trong 5 phút
- Action: Gửi SNS notification

#### Tiếp theo

Chuyển sang bước tiếp theo để thiết lập CloudFront distribution cho frontend.
