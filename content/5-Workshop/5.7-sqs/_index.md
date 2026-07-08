---
title: "Setting up Amazon SQS"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

#### Introduction to Amazon SQS

Amazon Simple Queue Service (SQS) is a fully managed message queue service. In ITCoach, SQS is used to:
- Asynchronously process heavy AI tasks (OpenAI STT + Evaluation + Polly)
- Separate fast API response from slow AI processing
- Ensure messages aren't lost if Lambda fails

#### SQS Architecture in ITCoach

```
User submit answer
    ↓
itcoach-answer-handler (Lambda)
    ├──→ DynamoDB (save answer)
    ├──→ SQS (send message)
    └──→ Return response immediately (don't wait for AI)

SQS Queue
    ↓ trigger
itcoach-ai-processor (Lambda)
    ├──→ OpenAI (STT + Evaluate)
    ├──→ Polly (Text-to-Speech)
    └──→ DynamoDB (update result)
```

#### Content

1. [Create Dead Letter Queue (DLQ)](5.7.1-dlq/)
2. [Create Main Processing Queue](5.7.2-main-queue/)
