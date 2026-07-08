---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Xây dựng nền tảng ITCoach với AWS Serverless

#### Tổng quan

**ITCoach** là nền tảng luyện phỏng vấn IT thông minh ứng dụng AI, được xây dựng hoàn toàn trên kiến trúc AWS Serverless. Trong workshop này, bạn sẽ học cách thiết lập từng thành phần của hệ thống từ đầu đến cuối bằng AWS Console.

Hệ thống bao gồm:
- **Frontend**: React + TypeScript phân phối qua CloudFront và S3
- **Backend**: 8 Lambda functions xử lý nghiệp vụ
- **Database**: 8 bảng DynamoDB lưu trữ dữ liệu
- **Authentication**: Amazon Cognito quản lý người dùng
- **Security**: AWS WAF bảo vệ CloudFront và API Gateway
- **AI Integration**: OpenAI API và Amazon Polly
- **Async Processing**: SQS xử lý tác vụ nặng
- **DNS & SSL**: Route 53 và ACM quản lý domain và chứng chỉ
- **Monitoring**: CloudWatch và SNS

#### Nội dung

1. [Tổng quan về workshop](5.1-Workshop-overview/)
2. [Chuẩn bị](5.2-Prerequiste/)
3. [Thiết lập IAM Role](5.3-iam-role/)
4. [Tạo S3 Buckets](5.4-s3-buckets/)
5. [Tạo DynamoDB Tables](5.5-dynamodb/)
6. [Cấu hình Amazon Cognito](5.6-cognito/)
7. [Thiết lập Amazon SQS](5.7-sqs/)
8. [Tạo Lambda Functions](5.8-lambda/)
9. [Cấu hình API Gateway](5.9-api-gateway/)
10. [Thiết lập AWS WAF](5.10-waf/)
11. [Thiết lập CloudFront](5.11-cloudfront/)
12. [Cấu hình Route 53 và SSL](5.12-route53-ssl/)
13. [Monitoring với CloudWatch](5.13-monitoring/)
14. [Deploy Code](5.14-deploy-code/)
15. [Dọn dẹp tài nguyên](5.15-cleanup/)
