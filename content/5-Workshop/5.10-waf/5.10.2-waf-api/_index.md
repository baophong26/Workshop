---
title: "WAF for API Gateway"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.10.2. </b> "
---

#### WAF for API Gateway (Regional Scope)

WAF for API Gateway protects the backend API from direct attacks from the React + TypeScript app. Since the app calls API Gateway directly (not through CloudFront), we need a separate WAF for API Gateway.

#### API Gateway WAF Characteristics

- **Scope**: Regional (ap-southeast-1)
- **Manual creation**: Must create separate Web ACL and associate with API Gateway
- **Rules**: 3 managed rules + 2 rate-limit rules (general + auth endpoint)
- **Cost**: ~$5-10/month depending on traffic

#### Implementation Steps

**1. Access WAF Console**

- Search for **WAF** or **AWS WAF & Shield**
- Ensure Region: **Asia Pacific (Singapore) - ap-southeast-1**

**2. Create Web ACL**

- Click **Create Web ACL**

**Web ACL Details:**
- Name: `itcoach-api-waf`
- Resource type: **Regional resources**
- Region: **Asia Pacific (Singapore)**

**Associated AWS resources:**
- Click **Add AWS resources**
- Resource type: **API Gateway**
- Select previously created API Gateway stage: `itcoach-api/prod`
- Click **Add**

**3. Add Managed Rules**

Click **Add rules** → **Add managed rule groups**

Select these 3 managed rules:

**a) AWS Managed Rules - Core rule set**
- Name: `AWSManagedRulesCommonRuleSet`
- Protection: SQL Injection, XSS, Path Traversal
- Priority: 10

**b) AWS Managed Rules - Known bad inputs**
- Name: `AWSManagedRulesKnownBadInputsRuleSet`
- Protection: Known malicious patterns
- Priority: 20

**c) AWS Managed Rules - Amazon IP reputation list**
- Name: `AWSManagedRulesAmazonIpReputationList`
- Protection: Block bad IPs from Amazon list
- Priority: 30

**4. Add Rate Limit Rule - General**

Click **Add rules** → **Add my own rules and rule groups** → **Rule builder**

**General Rate Limit:**
- Name: `GeneralRateLimitRule`
- Type: **Rate-based rule**
- Rate limit: **2000 requests per 5 minutes per IP**
- Action: **Block**
- Priority: 40

**5. Add Rate Limit Rule - Auth Endpoint**

The `/auth` endpoint needs special protection against brute-force attacks.

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

This configuration limits each IP to only call `/auth` 20 times maximum in 5 minutes, preventing brute-force login attempts.

**6. Default Action**

- Default action: **Allow**
- Only block requests violating rules

**7. CloudWatch Metrics**

- Enable: **Amazon CloudWatch metrics**
- Metric name: `itcoach-api-waf`

**8. Review and Create**

- Review configuration
- Click **Create Web ACL**

**9. Verify Association**

Return to API Gateway Console:

- API Gateway → Stages → **prod**
- **Web ACL** tab
- Should see: `itcoach-api-waf`

#### Result

✅ API Gateway WAF is ready to protect the backend API

#### Information to Save

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

#### Test API Gateway WAF

**Test General Rate Limit:**

```bash
for i in {1..2100}; do curl -I https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod/questions; done
```

**Test Auth Rate Limit (more strict):**

```bash
for i in {1..25}; do curl -I https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod/auth; done
```

After 20 requests to `/auth` in 5 minutes, IP will be blocked.

#### CloudWatch Metrics

View WAF metrics at:

- CloudWatch → Metrics → **WAFV2**
- Region: **ap-southeast-1**
- Filter: `itcoach-api-waf`
- Metrics: AllowedRequests, BlockedRequests

#### CloudWatch Alarms (Optional)

Create alarm when blocked requests increase significantly:

- CloudWatch → Alarms → **Create alarm**
- Metric: `WAFV2 > itcoach-api-waf > BlockedRequests`
- Condition: `>= 100` in 5 minutes
- Action: Send SNS notification

#### Next Steps

Move to the next step to set up CloudFront distribution for the frontend.
