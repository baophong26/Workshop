---
title: "Giới thiệu"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

#### Giới thiệu về ITCoach

ITCoach là nền tảng luyện phỏng vấn IT thông minh ứng dụng AI, giúp sinh viên IT và người mới đi làm rèn luyện kỹ năng phỏng vấn thực tế. Nền tảng được xây dựng hoàn toàn trên kiến trúc AWS Serverless, đảm bảo:

- **Không cần quản lý server**: Lambda tự động xử lý và mở rộng
- **Chi phí thấp**: Pay-per-use, chỉ trả tiền khi sử dụng
- **Hiệu năng cao**: CloudFront phân phối toàn cầu
- **Bảo mật tốt**: Cognito và IAM quản lý truy cập

#### Yêu cầu trước khi bắt đầu

Để hoàn thành workshop này, bạn cần:

1. **Tài khoản AWS** với quyền Administrator hoặc đủ quyền tạo các dịch vụ sau:
   - IAM, S3, DynamoDB, Cognito, SQS, Lambda, API Gateway, CloudFront, Route 53, ACM, CloudWatch, SNS

2. **OpenAI API Key**: Đăng ký tại [platform.openai.com](https://platform.openai.com) để sử dụng Speech-to-Text và GPT evaluation (**Quan trọng**: phải có ít nhất **$5** credit)

3. **Region**: Workshop này sử dụng **ap-southeast-1 (Singapore)** cho hầu hết dịch vụ
   - **Đặc biệt**: ACM SSL Certificate phải tạo ở **us-east-1** để dùng với CloudFront

#### Tính năng chính

**1. Đa dạng hình thức luyện tập:**
- Quiz trắc nghiệm với Spaced Repetition SM-2
- Tự luận nhập văn bản hoặc ghi âm giọng nói
- Mô phỏng phỏng vấn thực tế với AI

**2. AI đánh giá thông minh:**
- OpenAI API chuyển giọng nói thành text
- AI chấm điểm và đưa feedback chi tiết
- Amazon Polly đọc phản hồi bằng giọng nói

**3. Gamification:**
- Hệ thống XP, level, badge
- Streak học liên tục
- Bảng xếp hạng cạnh tranh

**4. Dashboard cá nhân:**
- Theo dõi tiến độ học tập
- Phân tích điểm yếu
- Đề xuất nội dung ưu tiên ôn

#### Kiến trúc hệ thống

Trong workshop này, bạn sẽ xây dựng hệ thống với các thành phần:

- **Frontend**: React + TypeScript trên S3 + CloudFront
- **Backend**: 8 Lambda functions
- **Database**: 8 bảng DynamoDB
- **Authentication**: Amazon Cognito
- **Message Queue**: Amazon SQS
- **Security**: AWS WAF (2 Web ACLs cho CloudFront và API Gateway)
- **DNS & SSL**: Route 53 + ACM
- **Monitoring**: CloudWatch + SNS

![ITCoach Architecture](/images/ITCoachArchitecture.png)

*Lưu ý: Sơ đồ trên đã gộp các Lambda functions theo nhóm logic để dễ nhìn:*
- *"**AWS Lambda (8 functions)**" trong sơ đồ đại diện cho 7 Lambda sync: `auth-handler`, `question-handler`, `session-handler`, `answer-handler`, `quiz-handler`, `gamification-handler`, `leaderboard-handler`*
- *"**itcoach-ai-processor**" là Lambda async thứ 8, xử lý tác vụ AI nặng qua SQS*
- *Trong thực tế triển khai, mỗi function được tạo riêng biệt (best practice: least privilege, cold start optimization, dễ debug)*

#### Luồng xử lý chính

```
User (Browser)
    ↓ HTTPS – itcoach24h.xyz
Amazon Route 53 (DNS)
    ↓
AWS WAF (CloudFront - Global) ← Chặn SQL Injection, XSS, DDoS
    ↓
Amazon CloudFront (CDN) ←→ S3 Static (React + TypeScript)
    ↓
AWS WAF (API Gateway - Regional) ← Rate limiting /auth endpoint
    ↓
Amazon API Gateway (8 endpoints, Throttling: 100 req/s)
    ↓ Cognito Authorizer
AWS Lambda (8 functions)
    ├──→ DynamoDB (8 tables)
    ├──→ S3 Audio (Presigned URL)
    ├──→ SQS (Async Processing)
    │      ↓
    │   itcoach-ai-processor
    │      ├──→ OpenAI API (STT + Evaluation)
    │      └──→ Amazon Polly (Text-to-Speech)
    └──→ CloudWatch → SNS (Alerts)
```

#### Thời gian ước tính

- **Thiết lập hạ tầng AWS**: 1-2 giờ
- **Deploy code (sau khi dev xong)**: 30 phút
- **Testing và kiểm tra**: 30 phút

**Tổng thời gian**: 2-3 giờ

