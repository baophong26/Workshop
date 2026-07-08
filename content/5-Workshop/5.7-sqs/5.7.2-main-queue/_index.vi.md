---
title: "Tạo Main Processing Queue"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.7.2. </b> "
---

#### Mục đích Main Queue

Queue `itcoach-processing-queue` là queue chính nhận message từ Lambda `itcoach-answer-handler` và trigger Lambda `itcoach-ai-processor` để xử lý AI.

#### Các bước thực hiện

**1. Tạo Queue mới**

- Ở SQS Console, click **Create queue**

**2. Cấu hình Main Queue**

**Type:**
- Chọn **Standard**

**Name:**
- Queue name: `itcoach-processing-queue`

**Configuration:**
- **Visibility timeout: `300` seconds** (5 phút - cho Lambda xử lý AI)
- Message retention period: `1` day (giữ message 1 ngày)
- Delivery delay: `0` seconds
- Maximum message size: 256 KB (mặc định)
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
- Chọn `itcoach-dlq` vừa tạo
- **Maximum receives: `3`** (thử lại tối đa 3 lần trước khi chuyển vào DLQ)

![Main Queue Config](/images/5-Workshop/5.7-sqs/002-main-queue-config.png)

- Click **Create queue**

**3. Lưu Queue URL**

Sau khi tạo xong:
- Copy **URL** của queue
- Dạng: `https://sqs.ap-southeast-1.amazonaws.com/ACCOUNT_ID/itcoach-processing-queue`

#### Kết quả

✅ Main Queue `itcoach-processing-queue` với DLQ đã được cấu hình

#### Thông tin cần lưu

```
Queue Name: itcoach-processing-queue
Queue URL: https://sqs.ap-southeast-1.amazonaws.com/ACCOUNT_ID/itcoach-processing-queue
Visibility Timeout: 300 seconds
DLQ: itcoach-dlq (max 3 receives)
```


#### Luồng xử lý message

1. **itcoach-answer-handler** gửi message vào queue
2. Message chờ trong queue
3. **itcoach-ai-processor** được trigger tự động (SQS Lambda trigger)
4. Lambda xử lý message (OpenAI + Polly)
5. Nếu thành công: message bị xóa khỏi queue
6. Nếu lỗi: message được thử lại (tối đa 3 lần)
7. Sau 3 lần lỗi: message chuyển sang DLQ

#### Tiếp theo

Chuyển sang bước tiếp theo để tạo Lambda Functions.

