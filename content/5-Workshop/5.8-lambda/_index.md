---
title: "Creating Lambda Functions"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

#### Introduction to AWS Lambda

AWS Lambda is a serverless compute service that lets you run code without managing servers. Lambda automatically scales and you only pay for actual compute time.

#### List of 8 Lambda Functions

| # | Function Name | Task |
|---|--------------|------|
| 1 | `itcoach-auth-handler` | Registration, login, profile management |
| 2 | `itcoach-question-handler` | Get essay questions + topic lists |
| 3 | `itcoach-session-handler` | Create and manage Mock Interview sessions |
| 4 | `itcoach-answer-handler` | Receive answers, create Presigned URL for audio upload |
| 5 | `itcoach-ai-processor` | OpenAI STT + evaluation + Polly TTS (async from SQS) |
| 6 | `itcoach-result-handler` | Return results, scores, history, statistics |
| 7 | `itcoach-quiz-handler` | Quiz multiple choice + SM-2 + add XP |
| 8 | `itcoach-gamification-handler` | XP, level, streak, leaderboard |

#### Process to create 1 Lambda (repeat 8 times)

**Step 1: Create function**
- Runtime: **Python 3.12**
- Execution role: **Use existing role** → select `itcoach-lambda-role`

**Step 2: Placeholder code**
- Deploy placeholder code with CORS headers

**Step 3: Configuration**
- Timeout: **30 seconds**
- Memory: **256 MB**

**Step 4: Environment variables**
- Add env vars per function (see details in step 5.8.2)

**Step 5: SQS Trigger (only for ai-processor)**
- Connect SQS queue to `itcoach-ai-processor`


#### Content

1. [Create 8 Lambda Functions](5.8.1-create-functions/)
2. [Configure Environment Variables](5.8.2-env-vars/)
3. [Connect SQS Trigger](5.8.3-sqs-trigger/)
