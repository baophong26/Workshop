---
title: "Create Gamification Table"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 5.5.8. </b> "
---

#### Purpose

The `itcoach-gamification` table stores XP, level, streak, and badges for each user. Also used to create leaderboards.

#### Table Configuration

- Table name: `itcoach-gamification`
- Partition key: `userId` - **String**
- Sort key: *(none)*
- Capacity mode: **On-demand**

#### Create Global Secondary Index for Leaderboard

After table is Active:

1. **Indexes** tab → **Create index**

**Special configuration:**
- Partition key: `type` - **String**
- Sort key: `xp` - **Number**
- Index name: `xp-index`

![Gamification XP Index](/images/5-Workshop/5.5-dynamodb/006-table-gamification-xp-index.png)

2. **Create index**


#### Sample Data Structure

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

#### Result

✅ Table `itcoach-gamification` with GSI `xp-index` for leaderboard

#### DynamoDB Summary

Completed creating **8 DynamoDB tables** for the ITCoach system! 🎉

| # | Table | PK | SK | GSI | Status |
|---|-------|----|----|-----|--------|
| 1 | itcoach-users | userId | - | - | ✅ |
| 2 | itcoach-questions | questionId | - | category-index | ✅ |
| 3 | itcoach-sessions | sessionId | - | userId-index | ✅ |
| 4 | itcoach-answers | answerId | - | sessionId-index | ✅ |
| 5 | itcoach-history | userId | timestamp | - | ✅ |
| 6 | itcoach-topics | specialty | topicId | - | ✅ |
| 7 | itcoach-quiz-attempts | userId | questionId | - | ✅ |
| 8 | itcoach-gamification | userId | - | xp-index | ✅ |
