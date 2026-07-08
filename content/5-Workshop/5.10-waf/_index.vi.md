---
title: "AWS WAF"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 5.10. </b> "
---

#### Giới thiệu về AWS WAF

AWS WAF (Web Application Firewall) là tường lửa ứng dụng web giúp bảo vệ hệ thống khỏi các cuộc tấn công phổ biến như SQL Injection, Cross-Site Scripting (XSS), và DDoS.

Trong hệ thống ITCoach, chúng ta cần **2 Web ACL riêng biệt**:
- **WAF cho CloudFront** (Global scope - us-east-1): Bảo vệ frontend
- **WAF cho API Gateway** (Regional scope - ap-southeast-1): Bảo vệ backend API

#### Tại sao cần 2 Web ACL?

1. **CloudFront** là Global service → WAF phải tạo ở **us-east-1**
2. **API Gateway** là Regional service → WAF phải tạo ở **ap-southeast-1**
3. App React gọi **trực tiếp** API Gateway (không qua CloudFront) → cần bảo vệ riêng
4. AWS không cho phép dùng chung 1 Web ACL cho cả 2 scope khác nhau

#### Nội dung

1. [WAF cho CloudFront (Global)](5.10.1-waf-cloudfront/)
2. [WAF cho API Gateway (Regional)](5.10.2-waf-api/)

#### Lợi ích của WAF

- Chặn SQL Injection, XSS tự động
- Chặn IP xấu từ danh sách Amazon
- Giới hạn số request/IP chống DDoS
- Bảo vệ endpoint `/auth` khỏi brute-force
- Cảnh báo qua CloudWatch khi bị tấn công

#### Chi phí WAF

- Web ACL CloudFront: Miễn phí trong Free plan (tối đa 5 rules)
- Web ACL API Gateway: ~$5/tháng + ~$1/rule/tháng
- Tổng ước tính: ~$10-15/tháng tuỳ traffic
