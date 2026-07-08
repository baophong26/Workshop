---
title: "Configuring API Gateway"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

#### Introduction to API Gateway

Amazon API Gateway is a service to create, publish, maintain, monitor, and secure APIs. In ITCoach, API Gateway will:
- Create 8 REST endpoints for frontend to call
- Authenticate requests via Cognito Authorizer
- Route requests to the right Lambda functions
- Enable CORS for browser

#### API Architecture

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

#### Content

1. [Create REST API](5.9.1-create-api/)
2. [Create Cognito Authorizer](5.9.2-authorizer/)
3. [Create 8 Resources and Methods](5.9.3-resources/)
4. [Deploy API](5.9.4-deploy/)
