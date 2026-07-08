---
title: "Thiết lập Amazon SQS"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

#### Giới thiệu về Amazon SQS

Amazon Simple Queue Service (SQS) là dịch vụ message queue được quản lý hoàn toàn. Trong ITCoach, SQS dùng để:
- Xử lý bất đồng bộ các tác vụ AI nặng (OpenAI STT + Evaluation + Polly)
- Tách biệt API response nhanh với AI processing chậm
- Đảm bảo message không bị mất nếu Lambda lỗi

#### Kiến trúc SQS trong ITCoach

```
User submit answer
    ↓
itcoach-answer-handler (Lambda)
    ├──→ DynamoDB (save answer)
    ├──→ SQS (send message)
    └──→ Return response ngay (không chờ AI)

SQS Queue
    ↓ trigger
itcoach-ai-processor (Lambda)
    ├──→ OpenAI (STT + Evaluate)
    ├──→ Polly (Text-to-Speech)
    └──→ DynamoDB (update result)
```

#### Nội dung

1. [Tạo Dead Letter Queue (DLQ)](5.7.1-dlq/)
2. [Tạo Main Processing Queue](5.7.2-main-queue/)

