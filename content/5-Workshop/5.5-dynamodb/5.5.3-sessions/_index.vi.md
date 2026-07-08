---
title: "Tạo bảng Sessions"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.5.3. </b> "
---

#### Mục đích

Bảng `itcoach-sessions` lưu trữ các phiên mô phỏng phỏng vấn (Mock Interview). Mỗi session lưu cấu hình (specialty, level, duration) và danh sách câu hỏi AI đã chọn.

#### Cấu hình Table

- Table name: `itcoach-sessions`
- Partition key: `sessionId` - **String**
- Sort key: *(không có)*
- Capacity mode: **On-demand**

#### Tạo Global Secondary Index

Sau khi table Active:

1. Tab **Indexes** → **Create index**
2. Partition key: `userId` - **String**
3. Index name: `userId-index`
4. **Create index**


#### Cấu trúc dữ liệu mẫu

```json
{
  "sessionId": "session-abc123",
  "userId": "user-123456",
  "specialty": "frontend",
  "level": "fresher",
  "duration": 30,
  "questions": ["q_fe_001", "q_fe_002", "q_fe_003"],
  "status": "in_progress",
  "startedAt": "2026-07-05T10:00:00Z",
  "totalScore": 75
}
```

#### Kết quả

✅ Bảng `itcoach-sessions` với GSI `userId-index`

