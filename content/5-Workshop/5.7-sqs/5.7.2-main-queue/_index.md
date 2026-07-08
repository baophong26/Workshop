---
title: "Create Main Processing Queue"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.7.2. </b> "
---

#### Purpose of Main Queue

The `itcoach-processing-queue` is the main queue that receives messages from Lambda `itcoach-answer-handler` and triggers Lambda `itcoach-ai-processor` for AI processing.

#### Steps

**1. Create New Queue**

- In SQS Console, click **Create queue**

**2. Configure Main Queue**

**Type:**
- Select **Standard**

**Name:**
- Queue name: `itcoach-processing-queue`

**Configuration:**
- **Visibility timeout: `300` seconds** (5 minutes - for Lambda AI processing)
- Message retention period: `1` day (keep messages for 1 day)
- Delivery delay: `0` seconds
- Maximum message size: 256 KB (default)
- Receive message wait time: 0 seconds

**Encryption:**
- Server-side encryption: **Enabled**
- Encryption key type: **Amazon SQS key (SSE-SQS)**

**Access policy:**
- Method: **Basic**
- Define who can send/receive: **Only queue owner**

**Dead-letter queue:**
- **Enabled** ✅
- Click **Choose queue**
- Select `itcoach-dlq` just created
- **Maximum receives: `3`** (retry max 3 times before moving to DLQ)

![Main Queue Config](/images/5-Workshop/5.7-sqs/002-main-queue-config.png)

- Click **Create queue**

**3. Save Queue URL**

After creation:
- Copy the queue **URL**
- Format: `https://sqs.ap-southeast-1.amazonaws.com/ACCOUNT_ID/itcoach-processing-queue`

#### Result

✅ Main Queue `itcoach-processing-queue` with DLQ configured

#### Information to Save

```
Queue Name: itcoach-processing-queue
Queue URL: https://sqs.ap-southeast-1.amazonaws.com/ACCOUNT_ID/itcoach-processing-queue
Visibility Timeout: 300 seconds
DLQ: itcoach-dlq (max 3 receives)
```


#### Message Processing Flow

1. **itcoach-answer-handler** sends message to queue
2. Message waits in queue
3. **itcoach-ai-processor** is triggered automatically (SQS Lambda trigger)
4. Lambda processes message (OpenAI + Polly)
5. If successful: message is deleted from queue
6. If error: message is retried (max 3 times)
7. After 3 failed attempts: message moves to DLQ

#### Next Steps

Move to the next step to create Lambda Functions.
