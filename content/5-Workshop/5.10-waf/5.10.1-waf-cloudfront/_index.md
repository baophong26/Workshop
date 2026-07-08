---
title: "WAF for CloudFront"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.10.1. </b> "
---

#### WAF for CloudFront (Global Scope)

WAF for CloudFront protects the React + TypeScript frontend from attacks like SQL Injection, XSS, and DDoS.

#### CloudFront WAF Characteristics

- **Scope**: Global (us-east-1)
- **Auto-creation**: CloudFront can automatically create Web ACL when enabling WAF
- **Rules**: 3 managed rules + 1 rate-limit rule
- **Cost**: Free in Free Tier (up to 5 rules)

#### Implementation Steps

**1. Access CloudFront Console**

- Search for **CloudFront**
- Click on the previously created Distribution

**2. Enable WAF for CloudFront**

- **Security** tab → **AWS WAF**
- Click **Enable AWS WAF**
- Select **Create new Web ACL**

**3. Configure Web ACL**

**Web ACL Details:**
- Name: `itcoach-cloudfront-waf`
- Resource type: **CloudFront distributions**
- Region: **Global (CloudFront)**

**4. Add Managed Rules**

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

**5. Add Rate Limit Rule**

Click **Add rules** → **Add my own rules and rule groups** → **Rule builder**

**Rate Limit Rule:**
- Name: `RateLimitRule`
- Type: **Rate-based rule**
- Rate limit: **2000 requests per 5 minutes per IP**
- Action: **Block**
- Priority: 40

**6. Default Action**

- Default action: **Allow**
- Only block requests violating rules

**7. Review and Create**

- Review configuration
- Click **Create Web ACL**

**8. Associate with CloudFront**

Web ACL will automatically associate with CloudFront distribution. Verify:

- **Associated AWS resources** tab
- CloudFront distribution must appear in the list

#### Result

✅ CloudFront WAF is ready to protect the frontend

#### Information to Save

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

#### Test CloudFront WAF

Access CloudFront domain multiple times consecutively to test rate limit:

```bash
for i in {1..2100}; do curl -I https://xxxxxxxxxxxx.cloudfront.net; done
```

After 2000 requests in 5 minutes, IP will be temporarily blocked.

#### CloudWatch Metrics

View WAF metrics at:

- CloudWatch → Metrics → **WAF**
- Filter: `itcoach-cloudfront-waf`
- Metrics: AllowedRequests, BlockedRequests, CountedRequests

#### Next Steps

Move to the next step to set up WAF for API Gateway (Regional scope).
