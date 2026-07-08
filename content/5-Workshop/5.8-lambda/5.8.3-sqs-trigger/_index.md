---
title: "Connect SQS Trigger"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.8.3. </b> "
---

#### Purpose

Connect SQS queue `itcoach-processing-queue` as a trigger for Lambda `itcoach-ai-processor`. When there's a message in the queue, Lambda will be automatically invoked.

#### Steps

**1. Go to Lambda itcoach-ai-processor**

- Click on function `itcoach-ai-processor`

**2. Add Trigger**

- **Configuration** tab → **Triggers** → **Add trigger**

**3. Configure SQS Trigger**

- Trigger configuration → select **SQS**
- SQS queue: select **`itcoach-processing-queue`**
- Batch size: `1` (process 1 message at a time)
- Enabled: ✅

![SQS Trigger](/images/5-Workshop/5.8-lambda/004-sqs-trigger.png)

- Click **Add**

**4. Verify Trigger**

After adding, you'll see the SQS trigger in Function overview.

#### Result

✅ Lambda `itcoach-ai-processor` will automatically run when there's a message in SQS queue

#### How It Works

1. `itcoach-answer-handler` sends message to SQS
2. SQS automatically triggers `itcoach-ai-processor`
3. Lambda receives message, processes AI (OpenAI + Polly)
4. If successful: message is deleted
5. If error: message retries (max 3 times) then moves to DLQ

#### Lambda Summary

Completed **8 Lambda functions** for ITCoach system! 🎉

| # | Function | Role | Timeout | Env Vars | Trigger |
|---|----------|------|---------|----------|---------|
| 1 | itcoach-auth-handler | ✅ | ✅ | - | API Gateway |
| 2 | itcoach-question-handler | ✅ | ✅ | - | API Gateway |
| 3 | itcoach-session-handler | ✅ | ✅ | ✅ | API Gateway |
| 4 | itcoach-answer-handler | ✅ | ✅ | ✅ | API Gateway |
| 5 | itcoach-ai-processor | ✅ | ✅ | ✅ | **SQS** ✅ |
| 6 | itcoach-result-handler | ✅ | ✅ | ✅ | API Gateway |
| 7 | itcoach-quiz-handler | ✅ | ✅ | ✅ | API Gateway |
| 8 | itcoach-gamification-handler | ✅ | ✅ | ✅ | API Gateway |
