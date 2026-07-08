---
title: "Cấu hình Environment Variables"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.8.2. </b> "
---

#### Giới thiệu

Environment Variables cho phép Lambda truy cập các thông tin như tên bảng DynamoDB, S3 bucket, SQS URL mà không cần hardcode trong code.

#### Cách thêm Environment Variables

1. Vào từng Lambda function
2. Tab **Configuration** → **Environment variables** → **Edit**
3. Click **Add environment variable**
4. Nhập **Key** và **Value**
5. Click **Save**

![Env Vars](/images/5-Workshop/5.8-lambda/003-env-vars.png)

#### Environment Variables cho từng Function

### itcoach-answer-handler

| Key | Value |
|-----|-------|
| `REGION` | `ap-southeast-1` |
| `S3_AUDIO_BUCKET` | `itcoach-audio-upload` |
| `DYNAMODB_TABLE_ANSWERS` | `itcoach-answers` |
| `DYNAMODB_TABLE_SESSIONS` | `itcoach-sessions` |
| `SQS_QUEUE_URL` | `https://sqs.ap-southeast-1.amazonaws.com/[ACCOUNT]/itcoach-processing-queue` |

### itcoach-ai-processor

| Key | Value |
|-----|-------|
| `REGION` | `ap-southeast-1` |
| `OPENAI_API_KEY` | `sk-xxxxxxxxx` ← **điền key thật của bạn** |
| `S3_AUDIO_BUCKET` | `itcoach-audio-upload` |
| `DYNAMODB_TABLE_ANSWERS` | `itcoach-answers` |
| `DYNAMODB_TABLE_HISTORY` | `itcoach-history` |

### itcoach-result-handler

| Key | Value |
|-----|-------|
| `REGION` | `ap-southeast-1` |
| `DYNAMODB_TABLE_ANSWERS` | `itcoach-answers` |
| `DYNAMODB_TABLE_SESSIONS` | `itcoach-sessions` |
| `DYNAMODB_TABLE_HISTORY` | `itcoach-history` |

### itcoach-session-handler

| Key | Value |
|-----|-------|
| `REGION` | `ap-southeast-1` |
| `DYNAMODB_TABLE_SESSIONS` | `itcoach-sessions` |
| `DYNAMODB_TABLE_QUESTIONS` | `itcoach-questions` |
| `DYNAMODB_TABLE_TOPICS` | `itcoach-topics` |

### itcoach-quiz-handler

| Key | Value |
|-----|-------|
| `REGION` | `ap-southeast-1` |
| `DYNAMODB_TABLE_QUESTIONS` | `itcoach-questions` |
| `DYNAMODB_TABLE_QUIZ_ATTEMPTS` | `itcoach-quiz-attempts` |
| `DYNAMODB_TABLE_GAMIFICATION` | `itcoach-gamification` |
| `DYNAMODB_TABLE_TOPICS` | `itcoach-topics` |

### itcoach-gamification-handler

| Key | Value |
|-----|-------|
| `REGION` | `ap-southeast-1` |
| `DYNAMODB_TABLE_GAMIFICATION` | `itcoach-gamification` |
| `DYNAMODB_TABLE_USERS` | `itcoach-users` |
| `DYNAMODB_TABLE_HISTORY` | `itcoach-history` |


#### Kết quả

✅ Tất cả Lambda functions đã có environment variables cần thiết

