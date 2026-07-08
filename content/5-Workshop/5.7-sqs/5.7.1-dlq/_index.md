---
title: "Create Dead Letter Queue"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.7.1. </b> "
---

#### Purpose of Dead Letter Queue

**DLQ (Dead Letter Queue)** is a backup queue that stores failed messages after multiple retry attempts. It helps:
- Not lose important messages
- Debug errors more easily
- Separate failed messages from main queue


#### Steps

**1. Access SQS Console**

- Search for **SQS** in search bar
- Click on **Amazon SQS**

**2. Create Queue**

- Click **Create queue**

**3. Configure DLQ**

**Type:**
- Select **Standard** (no need for FIFO in this workshop)

**Name:**
- Queue name: `itcoach-dlq`

**Configuration:**
- Keep all defaults
- Visibility timeout: 30 seconds
- Message retention period: 4 days
- Delivery delay: 0 seconds

**Encryption:**
- Server-side encryption: **Enabled**
- Encryption key type: **Amazon SQS key (SSE-SQS)**

**Access policy:**
- Method: **Basic**
- Define who can send/receive: **Only queue owner**

- Click **Create queue**

**4. Save DLQ ARN**

After creation:
- Copy the **ARN** of DLQ
- Format: `arn:aws:sqs:ap-southeast-1:ACCOUNT_ID:itcoach-dlq`

![DLQ Created](/images/5-Workshop/5.7-sqs/001-dlq-created.png)

#### Result

✅ Dead Letter Queue `itcoach-dlq` created

#### Information to Save

```
Queue Name: itcoach-dlq
ARN: arn:aws:sqs:ap-southeast-1:ACCOUNT_ID:itcoach-dlq
Type: Standard
```

#### Next Steps

Move to the next step to create Main Processing Queue.
