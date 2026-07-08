---
title: "Monitoring with CloudWatch"
date: 2024-01-01
weight: 13
chapter: false
pre: " <b> 5.13. </b> "
---

#### Introduction to Monitoring

Monitoring helps you track system health and receive alerts when issues occur. We will set up:
- **SNS Topic**: Receive email alerts
- **CloudWatch Alarms**: Detect Lambda errors, API Gateway, SQS


#### Part 1: Create SNS Topic

**1. Access SNS Console**

- Search for **SNS** → **Topics** → **Create topic**

![SNS Console](/images/5-Workshop/5.11-monitoring/001-sns-subscription.png)

**2. Configure Topic**

- Type: **Standard**
- Name: `itcoach-alerts`
- Display name: `ITCoach Alerts`
- Click **Create topic**

**3. Create Subscription**

- Click **Create subscription**
- Protocol: **Email**
- Endpoint: enter your email
- Click **Create subscription**

**4. Confirm Email (IMPORTANT)**

- Check email inbox
- Find email from AWS Notifications
- Click link **Confirm subscription**

Status will change from **Pending confirmation** → **Confirmed**

#### Part 2: CloudWatch Alarms (create after code deployment)


**Alarm 1: Lambda AI Errors**

- Service: Lambda
- Function: `itcoach-ai-processor`
- Metric: `Errors`
- Condition: `> 5` in 5 minutes
- Action: SNS `itcoach-alerts`

**Alarm 2: API Gateway 5xx Errors**

- Service: API Gateway
- API: `itcoach-api`
- Metric: `5XXError`
- Condition: `> 10` in 5 minutes
- Action: SNS `itcoach-alerts`

**Alarm 3: SQS Message Backlog**

- Service: SQS
- Queue: `itcoach-processing-queue`
- Metric: `ApproximateNumberOfMessagesVisible`
- Condition: `> 50` in 5 minutes
- Action: SNS `itcoach-alerts`

#### Result

✅ SNS Topic `itcoach-alerts` ready to receive email alerts

#### Information to Save

```
SNS Topic: itcoach-alerts
Subscription: Email confirmed
CloudWatch Alarms: Create after code deployment
```

#### Next Steps

Move to the final part - Cleanup resources.
