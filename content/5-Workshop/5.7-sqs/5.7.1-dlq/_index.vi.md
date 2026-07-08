---
title: "Tạo Dead Letter Queue"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.7.1. </b> "
---

#### Mục đích Dead Letter Queue

**DLQ (Dead Letter Queue)** là queue dự phòng lưu các message bị lỗi sau nhiều lần thử lại. Giúp:
- Không mất message quan trọng
- Debug lỗi dễ dàng hơn
- Tách riêng message lỗi khỏi queue chính


#### Các bước thực hiện

**1. Truy cập SQS Console**

- Tìm kiếm **SQS** trong thanh tìm kiếm
- Click vào **Amazon SQS**

**2. Tạo Queue**

- Click **Create queue**

**3. Cấu hình DLQ**

**Type:**
- Chọn **Standard** (không cần FIFO cho workshop này)

**Name:**
- Queue name: `itcoach-dlq`

**Configuration:**
- Giữ mặc định tất cả
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

**4. Lưu DLQ ARN**

Sau khi tạo xong:
- Copy **ARN** của DLQ
- Dạng: `arn:aws:sqs:ap-southeast-1:ACCOUNT_ID:itcoach-dlq`

![DLQ Created](/images/5-Workshop/5.7-sqs/001-dlq-created.png)

#### Kết quả

✅ Dead Letter Queue `itcoach-dlq` đã được tạo

#### Thông tin cần lưu

```
Queue Name: itcoach-dlq
ARN: arn:aws:sqs:ap-southeast-1:ACCOUNT_ID:itcoach-dlq
Type: Standard
```

#### Tiếp theo

Chuyển sang bước tiếp theo để tạo Main Processing Queue.

