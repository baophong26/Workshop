---
title: "Monitoring với CloudWatch"
date: 2024-01-01
weight: 13
chapter: false
pre: " <b> 5.13. </b> "
---

#### Giới thiệu về Monitoring

Monitoring giúp bạn theo dõi sức khỏe hệ thống và nhận cảnh báo khi có vấn đề. Chúng ta sẽ thiết lập:
- **SNS Topic**: Nhận email cảnh báo
- **CloudWatch Alarms**: Phát hiện lỗi Lambda, API Gateway, SQS


#### Phần 1: Tạo SNS Topic

**1. Truy cập SNS Console**

- Tìm kiếm **SNS** → **Topics** → **Create topic**

![SNS Console](/images/5-Workshop/5.11-monitoring/001-sns-subscription.png)

**2. Cấu hình Topic**

- Type: **Standard**
- Name: `itcoach-alerts`
- Display name: `ITCoach Alerts`
- Click **Create topic**

**3. Tạo Subscription**

- Click **Create subscription**
- Protocol: **Email**
- Endpoint: nhập email của bạn
- Click **Create subscription**

**4. Xác nhận Email (QUAN TRỌNG)**

- Vào email inbox
- Tìm email từ AWS Notifications
- Click link **Confirm subscription**

Status sẽ chuyển từ **Pending confirmation** → **Confirmed**

#### Phần 2: CloudWatch Alarms (tạo sau khi có code)


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

#### Kết quả

✅ SNS Topic `itcoach-alerts` đã sẵn sàng nhận email cảnh báo

#### Thông tin cần lưu

```
SNS Topic: itcoach-alerts
Subscription: Email confirmed
CloudWatch Alarms: Tạo sau khi deploy code
```

#### Tiếp theo

Chuyển sang phần cuối cùng - Cleanup resources.

