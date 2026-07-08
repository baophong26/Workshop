---
title: "Tạo bảng History"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5.5. </b> "
---

#### Mục đích

Bảng `itcoach-history` lưu lịch sử học tập hàng ngày để hiển thị dashboard và thống kê tiến độ.

#### Cấu hình Table

- Table name: `itcoach-history`
- Partition key: `userId` - **String**
- Sort key: `timestamp` - **String**
- Capacity mode: **On-demand**


#### Không cần Global Secondary Index

Bảng này không cần GSI vì luôn query theo `userId` (partition key).

#### Cấu trúc dữ liệu mẫu

```json
{
  "userId": "user-123456",
  "timestamp": "2026-07-05T10:00:00Z",
  "activityType": "quiz",
  "itemsCompleted": 10,
  "xpEarned": 50,
  "averageScore": 8.2,
  "timeSpentMinutes": 25
}
```

#### Kết quả

✅ Bảng `itcoach-history` với Partition Key + Sort Key

