---
title: "Tạo Lambda Functions"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

#### Giới thiệu về AWS Lambda

AWS Lambda là dịch vụ compute serverless cho phép chạy code mà không cần quản lý server. Lambda tự động scale và bạn chỉ trả phí cho thời gian compute thực tế.

#### Danh sách 8 Lambda Functions

| # | Function Name | Nhiệm vụ |
|---|--------------|----------|
| 1 | `itcoach-auth-handler` | Đăng ký, đăng nhập, quản lý profile |
| 2 | `itcoach-question-handler` | Lấy câu hỏi tự luận + danh sách topics |
| 3 | `itcoach-session-handler` | Tạo và quản lý phiên Mock Interview |
| 4 | `itcoach-answer-handler` | Nhận câu trả lời, tạo Presigned URL upload audio |
| 5 | `itcoach-ai-processor` | OpenAI STT + đánh giá + Polly TTS (async từ SQS) |
| 6 | `itcoach-result-handler` | Trả kết quả, điểm số, lịch sử, thống kê |
| 7 | `itcoach-quiz-handler` | Quiz trắc nghiệm + SM-2 + cộng XP |
| 8 | `itcoach-gamification-handler` | XP, level, streak, bảng xếp hạng |

#### Quy trình tạo 1 Lambda (lặp lại 8 lần)

**Bước 1: Create function**
- Runtime: **Python 3.12**
- Execution role: **Use existing role** → chọn `itcoach-lambda-role`

**Bước 2: Placeholder code**
- Deploy code placeholder có CORS headers

**Bước 3: Configuration**
- Timeout: **30 seconds**
- Memory: **256 MB**

**Bước 4: Environment variables**
- Thêm env vars theo từng function (xem chi tiết ở bước 5.8.2)

**Bước 5: SQS Trigger (chỉ cho ai-processor)**
- Kết nối SQS queue vào `itcoach-ai-processor`


#### Nội dung

1. [Tạo 8 Lambda Functions](5.8.1-create-functions/)
2. [Cấu hình Environment Variables](5.8.2-env-vars/)
3. [Kết nối SQS Trigger](5.8.3-sqs-trigger/)

