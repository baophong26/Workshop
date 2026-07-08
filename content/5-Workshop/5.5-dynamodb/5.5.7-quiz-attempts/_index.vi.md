---
title: "Tạo bảng Quiz Attempts"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.5.7. </b> "
---

#### Mục đích

Bảng `itcoach-quiz-attempts` lưu lịch sử làm quiz và các thông số cho thuật toán **Spaced Repetition SM-2** (interval, easeFactor, repetitions, nextReviewDate).

#### Cấu hình Table

- Table name: `itcoach-quiz-attempts`
- Partition key: `userId` - **String**
- Sort key: `questionId` - **String**
- Capacity mode: **On-demand**

#### Không cần Global Secondary Index

Không cần GSI vì luôn query theo `userId + questionId`.

#### Cấu trúc dữ liệu mẫu

```json
{
  "userId": "user-123456",
  "questionId": "q_fe_001",
  "lastAttemptDate": "2026-07-05",
  "lastResult": "correct",
  "totalAttempts": 3,
  "correctCount": 2,
  "interval": 7,
  "easeFactor": 2.5,
  "repetitions": 2,
  "nextReviewDate": "2026-07-12"
}
```

**Giải thích các field SM-2:**
- `interval`: Số ngày đến lần ôn tập tiếp theo
- `easeFactor`: Hệ số độ khó (2.5 là mặc định)
- `repetitions`: Số lần ôn tập liên tiếp đúng
- `nextReviewDate`: Ngày nên ôn lại câu này

#### Kết quả

✅ Bảng `itcoach-quiz-attempts` hỗ trợ Spaced Repetition

