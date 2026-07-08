---
title: "Create History Table"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5.5. </b> "
---

#### Purpose

The `itcoach-history` table stores daily learning history to display dashboard and progress statistics.

#### Table Configuration

- Table name: `itcoach-history`
- Partition key: `userId` - **String**
- Sort key: `timestamp` - **String**
- Capacity mode: **On-demand**

#### No Global Secondary Index Needed

This table doesn't need a GSI because queries are always by `userId` (partition key).

#### Sample Data Structure

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

#### Result

✅ Table `itcoach-history` with Partition Key + Sort Key
