---
title: "Kết nối SQS Trigger"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.8.3. </b> "
---

#### Mục đích

Kết nối SQS queue `itcoach-processing-queue` làm trigger cho Lambda `itcoach-ai-processor`. Khi có message trong queue, Lambda sẽ tự động được gọi.

#### Các bước thực hiện

**1. Vào Lambda itcoach-ai-processor**

- Click vào function `itcoach-ai-processor`

**2. Add Trigger**

- Tab **Configuration** → **Triggers** → **Add trigger**

**3. Cấu hình SQS Trigger**

- Trigger configuration → chọn **SQS**
- SQS queue: chọn **`itcoach-processing-queue`**
- Batch size: `1` (xử lý 1 message mỗi lần)
- Enabled: ✅

![SQS Trigger](/images/5-Workshop/5.8-lambda/004-sqs-trigger.png)

- Click **Add**

**4. Kiểm tra Trigger**

Sau khi thêm, bạn sẽ thấy SQS trigger trong Function overview.

#### Kết quả

✅ Lambda `itcoach-ai-processor` sẽ tự động chạy khi có message trong SQS queue

#### Cách hoạt động

1. `itcoach-answer-handler` gửi message vào SQS
2. SQS tự động trigger `itcoach-ai-processor`
3. Lambda nhận message, xử lý AI (OpenAI + Polly)
4. Nếu thành công: message bị xóa
5. Nếu lỗi: message retry (tối đa 3 lần) rồi chuyển DLQ

#### Tổng kết Lambda

Đã hoàn thành **8 Lambda functions** cho hệ thống ITCoach! 🎉

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

