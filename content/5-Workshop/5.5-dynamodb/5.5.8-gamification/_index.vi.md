---
title: "Tạo bảng Gamification"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 5.5.8. </b> "
---

#### Mục đích

Bảng `itcoach-gamification` lưu trữ XP, level, streak, badge của từng user. Cũng dùng để tạo bảng xếp hạng (leaderboard).

#### Cấu hình Table

- Table name: `itcoach-gamification`
- Partition key: `userId` - **String**
- Sort key: *(không có)*
- Capacity mode: **On-demand**

#### Tạo Global Secondary Index cho Leaderboard

Sau khi table Active:

1. Tab **Indexes** → **Create index**

**Cấu hình đặc biệt:**
- Partition key: `type` - **String**
- Sort key: `xp` - **Number**
- Index name: `xp-index`

![Gamification XP Index](/images/5-Workshop/5.5-dynamodb/006-table-gamification-xp-index.png)

2. **Create index**


#### Cấu trúc dữ liệu mẫu

```json
{
  "userId": "user-123456",
  "type": "USER",
  "xp": 1250,
  "level": 8,
  "currentStreak": 7,
  "longestStreak": 15,
  "badges": ["first-quiz", "week-warrior", "top-10"],
  "lastActiveDate": "2026-07-05",
  "rank": 42
}
```

#### Query Leaderboard

```javascript
// Query top 10 users by XP
const params = {
  TableName: 'itcoach-gamification',
  IndexName: 'xp-index',
  KeyConditionExpression: '#type = :userType',
  ExpressionAttributeNames: { '#type': 'type' },
  ExpressionAttributeValues: { ':userType': 'USER' },
  ScanIndexForward: false, // Sort descending
  Limit: 10
};
```

#### Kết quả

✅ Bảng `itcoach-gamification` với GSI `xp-index` cho leaderboard

#### Tổng kết DynamoDB

Đã tạo xong **8 bảng DynamoDB** cho hệ thống ITCoach! 🎉

| # | Bảng | PK | SK | GSI | Status |
|---|------|----|----|-----|--------|
| 1 | itcoach-users | userId | - | - | ✅ |
| 2 | itcoach-questions | questionId | - | category-index | ✅ |
| 3 | itcoach-sessions | sessionId | - | userId-index | ✅ |
| 4 | itcoach-answers | answerId | - | sessionId-index | ✅ |
| 5 | itcoach-history | userId | timestamp | - | ✅ |
| 6 | itcoach-topics | specialty | topicId | - | ✅ |
| 7 | itcoach-quiz-attempts | userId | questionId | - | ✅ |
| 8 | itcoach-gamification | userId | - | xp-index | ✅ |

