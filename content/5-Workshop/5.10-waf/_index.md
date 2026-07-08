---
title: "AWS WAF"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 5.10. </b> "
---

#### Introduction to AWS WAF

AWS WAF (Web Application Firewall) is a web application firewall that helps protect the system from common attacks like SQL Injection, Cross-Site Scripting (XSS), and DDoS.

In the ITCoach system, we need **2 separate Web ACLs**:
- **WAF for CloudFront** (Global scope - us-east-1): Protects frontend
- **WAF for API Gateway** (Regional scope - ap-southeast-1): Protects backend API

#### Why 2 Web ACLs?

1. **CloudFront** is a Global service → WAF must be created in **us-east-1**
2. **API Gateway** is a Regional service → WAF must be created in **ap-southeast-1**
3. React + TypeScript app calls API Gateway **directly** (not through CloudFront) → needs separate protection
4. AWS does not allow sharing 1 Web ACL across 2 different scopes

#### Contents

1. [WAF for CloudFront (Global)](5.10.1-waf-cloudfront/)
2. [WAF for API Gateway (Regional)](5.10.2-waf-api/)

#### Benefits of WAF

- Automatically blocks SQL Injection, XSS
- Blocks bad IPs from Amazon list
- Limits requests/IP to prevent DDoS
- Protects `/auth` endpoint from brute-force
- Alerts via CloudWatch when under attack

#### WAF Costs

- CloudFront Web ACL: Free in Free plan (up to 5 rules)
- API Gateway Web ACL: ~$5/month + ~$1/rule/month
- Total estimate: ~$10-15/month depending on traffic
