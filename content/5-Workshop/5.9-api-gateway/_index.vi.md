---
title: "Cấu hình API Gateway"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

#### Giới thiệu về API Gateway

Amazon API Gateway là dịch vụ tạo, publish, maintain, monitor và bảo mật APIs. Trong ITCoach, API Gateway sẽ:
- Tạo 8 REST endpoints cho frontend gọi
- Xác thực requests qua Cognito Authorizer
- Route requests đến đúng Lambda functions
- Enable CORS cho browser

#### Kiến trúc API

```
React + TypeScript Frontend
    ↓ HTTPS
API Gateway (8 endpoints)
    ├──→ /auth (POST) → itcoach-auth-handler (no auth)
    ├──→ /questions (GET) → itcoach-question-handler
    ├──→ /topics (GET) → itcoach-question-handler
    ├──→ /sessions (POST) → itcoach-session-handler
    ├──→ /answers (POST) → itcoach-answer-handler
    ├──→ /results (GET) → itcoach-result-handler
    ├──→ /quiz (POST) → itcoach-quiz-handler
    └──→ /leaderboard (GET) → itcoach-gamification-handler
```

#### Nội dung

1. [Tạo REST API](5.9.1-create-api/)
2. [Tạo Cognito Authorizer](5.9.2-authorizer/)
3. [Tạo 8 Resources và Methods](5.9.3-resources/)
4. [Deploy API](5.9.4-deploy/)

